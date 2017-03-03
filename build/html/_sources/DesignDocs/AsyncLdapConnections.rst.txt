Asynchronous LDAP connections
=============================

Problem Statement
-----------------

Currently, connecting to an LDAP server by the openldap library is
blocking. This means that when SSSD attempts to connect to an
unresponsive server, it can block up to 5 second (the current default
setting of ``ldap_network_timeout``). This is not ideal, as we would
like to be able to do something else while the connection is being made.

General Approach
----------------

Recent versions of openldap have a new (and not very well documented)
option ``LDAP_OPT_CONNECT_ASYNC`` that can be set by
``ldap_set_option()``. This option will cause all ldap functions that
create a new connection to only invoke ``connect()`` and not wait for
the socket to become ready for writing. If it is not, the function will
return ``LDAP_X_CONNECTING`` and it has to be executed again after the
socket becomes ready.

Implementation
--------------

Because a lot of ldap functions can cause the creation of a new socket,
every such function will be wrapped into a tevent\_req interface. Every
such wrapper will consist of a standard ``send`` and ``recv`` function,
as well as a so called ``try`` function.

The ``send`` function will copy all the arguments into the state data
structure and invoke the ``try`` function, passing the ``tevent_req`` to
it. The try function will invoke the openldap function with all the
arguments from the state. The ``try`` function will then return ``0`` if
``LDAP_X_CONNECTING`` was returned signaling that we will have to invoke
it one more time later. In case the connection was already available,
``tevent_req_done()`` or ``tevent_req_error()`` is invoked and ``1`` is
returned.

Callbacks
~~~~~~~~~

The implementation will make a heavy use of both openldap and tevent
callbacks. Our goal is to be able to invoke the ``try`` function from
the tevent callback (which will be invoked by tevent after the socket is
ready for writing). The main problem is to make both the ``try``
function and the ``tevent_req`` available to this callback. The
callbacks that we need work as follows:

#. Openldap callbacks are set by ``ldap_set_option()`` with the
   ``option`` argument set to ``LDAP_OPT_CONNECT_CB``. Additional data
   structure (\`struct ldap\_cb\_data\`) is passed in as well. This data
   structure will always be passed to the openldap callback. This is
   currently done in ``setup_ldap_connection_callbacks()``.
#. Right after an openldap function creates a connection, it will call
   the callback passing to it (among other things) the newly created
   socket. In SSSD, this callback is
   ``sdap_ldap_connect_callback_add()``.
#. The callback will then register a tevent callback
   ``sdap_ldap_result()`` which is invoked when the socket is ready for
   writing and is responsible for calling ``ldap_result()``.

What we need to do is to make sure that the tevent callback is called
not only when the socket is ready for reading, but also when it is ready
for writing (but only once, since it will always be ready for writing
after the connection is made). We also need to provide the tevent
callback with the ``try`` function and the associated ``tevent_req``
structure. After the socket is ready for writing, we call the ``try``
function and pass it the ``tevent_req`` so it can call the ldap function
again and mark the tevent request as finished.

To pass the tevent request to the tevent callback, we need to take a bit
of a detour. Every ``try`` function, before calling the ldap function
has to call ``set_fd_retry_cb()`` passing in a pointer to itself and the
tevent request. This function will save these to the data structure that
is available to the ldap callback. This callback is called after the
socket is created and in turn, the function pointer and the tevent
request are made available to the newly registered tevent callback,
which is what we wanted. The ``try`` function also has to call
``set_fd_retry_cb()`` again after the ldap function is called and set
both the function pointer and the tevent request pointer to ``NULL``. So
now when it's all set, after the socket is ready for writing we can call
the ``try`` function from the tevent callback to finish the whole
transaction.

Spies
-----

One problem with the approach described in the previous section is with
storing the tevent request in a place out of the tevent chain. If the
request gets freed before there is a chance to call the ``try``
function, we will be left with a dangling pointer that might eventually
be dereferenced.

To solve this problem, we create a sort of a "spy" that will free the
``fd_event_item`` associated with the tevent callback in case the
request is freed. The spy is created in the ldap callback. The following
diagram and code illustrate how the spy is used to make sure there are
no dangling pointers left:

.. raw:: html

   <div class="code">

::

    request_spy_destructor(struct request_spy *spy)
    {
        if (spy->ptr) {
            spy->ptr->spy = NULL;
            talloc_free(spy->ptr);
        }
    }

    fd_event_item_destructor(struct fd_event_item *fd_event_item)
    {
        if (fd_event_item->spy)
            fd_event_item->spy->ptr = NULL;
    }

.. raw:: html

   </div>
