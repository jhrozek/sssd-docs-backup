<div class="wiki-toc">

1.  [ELAPI Interface](#ELAPIInterface)
    1.  [Overview](#Overview)
    2.  [Architecture](#Architecture)
    3.  [ELAPI Concepts](#ELAPIConcepts)
        1.  [Event](#Event)
            1.  [Overview](#Overview1)
            2.  [Message attribute](#Messageattribute)
            3.  [Other special attributes](#Otherspecialattributes)
                1.  [`R_stamp__`](#R_stamp__)
                2.  [`R_time__`](#R_time__)
                3.  [`R_loco__`](#R_loco__)
            4.  [Event context](#Eventcontext)
        2.  [Event Template](#EventTemplate)
        3.  [Target](#Target)
            1.  [Overview](#Overview2)
            2.  [Internal Implementation](#InternalImplementation)
        4.  [Sink](#Sink)
            1.  [Overview](#Overview3)
            2.  [Internal Implementation](#InternalImplementation1)
            3.  [Sink Configuration](#SinkConfiguration)
        5.  [Providers](#Providers)
            1.  [Overview](#Overview4)
            2.  [Implementation](#Implementation)
                1.  [File Provider](#FileProvider)
                2.  [Supported formats](#Supportedformats)
                3.  [Append/Create? logic](#AppendCreatelogic)
                4.  [Configuration changes](#Configurationchanges)
                5.  [Special stderr
                    configuration](#Specialstderrconfiguration)
                6.  [Notion of sets](#Notionofsets)
        6.  [ELAPI Configuration](#ELAPIConfiguration)
        7.  [Dispatcher](#Dispatcher)
        8.  [Sync vs Async](#SyncvsAsync)
        9.  [Walk Through the Dispatcher Creation
            Call](#WalkThroughtheDispatcherCreationCall)
        10. [Walk Through the Synchronized Logging
            Call](#WalkThroughtheSynchronizedLoggingCall)
        11. [Walk Through the Asynchronous Logging
            Call](#WalkThroughtheAsynchronousLoggingCall)
        12. [Module List](#ModuleList)

</div>

ELAPI Interface {#ELAPIInterface}
===============

Overview {#Overview}
--------

**ELAPI** – stands for Event Logging API. There are many ways the
applications generate and submit the logging information. Historically
the applications usually write their log information to files, databases
or syslog. The need to collect and process these logs in one central
place for compliance and forensic reasons requires a new approach to the
logging of the information. The syslog is not good for processing due to
lack of specific format for the messages, there is no filtering at the
collection point and it is hard to filter unstructured data; the files
are hard to remote and merge in one central location; files also usually
do not have a well defined structured format.

The idea behind the ELAPI is to give the applications a mean to solve
several problems at the same time.

-   Applications usually lock on some logging interface like syslog,
    file and changing them to log into alternative more advanced log
    destination (log facility) becomes a challenge. The ELAPI solves
    this problem by creating a logging interface that would abstract the
    application from the actual destination of the log, it being a local
    file, syslog, database or something else. The log facilities (or
    sinks) can be plugged into the the ELAPI without any changes to the
    application.
-   The data that needs to be logged into the audit logs usually is
    complex and significantly varies from one situation the application
    deals with to another. It is very hard and some times impractical to
    create a fixed structure of the log messages (like in database
    cases) this usually ends up in situations when half of the fields is
    not used while the information has to be jammed into some fields
    since there is not clear definition of where it belongs to. The
    ELAPI solves this issue by providing the application a way to pass
    arbitrarily complex data to the logging facility. The data is
    represented by the collection of the key-value pairs. The
    collections can be easily constructed, modified or nested allowing
    reuse of the data in different events (for example the information
    about the peer host, or socket properties).
-   The information in the log should be complete but also human
    readable. In the ELAPI case this is achieved by separating the data
    of the event from the actual presentation (formatting) of the
    message. Thus the event can contain much more data than the message
    in a human readable form. The log facilities that work with human
    readable messages (syslog, file) will receive the event in the
    formatted, user readable form. The more advanced facilities like the
    one being built for IPA will receive the data and formatting
    information separately. Such approach allows much easier processing
    and filtering of the events based on raw data but leaves a
    possibility to convert the event into the human readable form at any
    moment when user wants to inspect the event.
-   Usually applications use different interfaces for logging, debugging
    and audit trails. This means that application developer needs to
    deal with three different way of emmiting information from the
    application. ELAPI comes to help providing one interface that can be
    configured to send events into different destinations. The event is
    a collection of key-value pairs. One of the keys is so called
    "target". The configuration can define different logical targets. By
    default ELAPI operates with three predefined targets "debug", "log"
    and "audit" but application developers can add other targets if they
    see a need to have more. Each target is represented by a number (for
    faster comparison) and mapped to a configuration in the ELAPI
    configuration file. If the event's value of the target attribute
    matches the number associated with the target in the configuration
    file (see specific details later), the event will be sent into this
    target.
-   The reliability of the target facilities is also very important. The
    audit information on one hand should not be lost but on the other
    logging should not be intrusive and prevent the application from
    doing what it is supposed to do. For that purpose the ELAPI allows
    defining several sinks (actual physical event destinations) per
    target. The sinks are listed in fail over order. If the active sink
    returns error and there is a fail over sink the ELAPI will
    automatically fail over without returning error. If there are no
    available sinks (all sinks returned error) and error will be
    returned to application and it is responsibility of the application
    to take a corresponding action.
-   As we started to implement ELAPI it turned out that it can also be
    used as a simple reporting tool. Any data that is read as key value
    pairs (database record for example) can be sent to the output
    destination (specifically file) in different formats (CSV, HTML
    etc.). Thus ELAPI can be used to create simple conversion tools that
    get data in one format and output using other. Though there are many
    other tools that do that it is useful to know that ELAPI is also an
    option.

Architecture {#Architecture}
------------

The following diagram illustrates the ELAPI architecture: []{}

So ELAPI is first of all an interface that allows applications to emit
logging, tracing, audit information. The interface consist of the core
part and couple different sets of wrappers that can be used by
application developers when they build threaded or non-threaded
applications.

Under the hood the ELAPI has a dispatcher. Dispatcher is the entity that
holds the targets, and sends the events to them evaluating which event
needs to go into which target. Targets consist of sink fail-over chains.
Same sink can be mentioned in chains belonging to different targets.
This capability should be used with cation so that events destined for
different targets might end up in one place. Sometimes this is desired
but some times not.

One of the main values of ELAPI is that targets and sinks can be
reconfigured at will without changing the application. New providers
(code that formats and writes events) can also be dropped in.

The original implementation includes following providers:

-   file provider - code that writes events to a file
-   syslog provider - code that writes events to the syslog

These providers (SUBJECT TO CHANGE) will be embedded directly into the
ELAPI itself. Other providers can be dropped in later.

One of such providers would be a so called IPA remote provider. This
provider will have a connection with the local collection daemon. This
daemon will get events from different ELAPI enabled applications that
send events through this "remote" provider, filter them and then deliver
to the central auditing server for storing and processing.

ELAPI Concepts {#ELAPIConcepts}
--------------

This section covers main concepts related to ELAPI.

### Event {#Event}

#### Overview {#Overview1}

**Event** - event is a collection of the key-value pairs. Application
creates a collection and sends it to log dispatcher (see below). There
are convenience APIs that allow doing it in one step
(creating-submitting-destroying).\
There are several special keys that have predefined meaning and use.
They are prefixed and suffixed with "`__`" or with "`R_`". The
attributes denoted by theses keys are common to many events. They are
defined in the
[common/elapi/elapi\_event.h](https://fedorahosted.org/sssd/browser/common/elapi/elapi_event.h){.source}.
See comments there.\
The attributes with "`__`" are just special "reserved" attributes. They
have prefix and suffix so that they are differentiated from the
attributes supplied by the application. The attributes with "`R_`" are
not only reserved attributes but also resolvable when the event is
submitted into dispatcher. This means that the value of the attribute is
set by ELAPI based on specific rules on per attribute basis.

#### Message attribute {#Messageattribute}

There is a special attribute named "`R_message__`" that can be a part of
any event. This attribute is processed differently than other
attributes. The message attribute can have place holders to reference
other attributes from the same event at the run time. For example the
message can be something like this:

``` {.wiki}
R_message___="This unfortunate event is logged on %(__host__) at %(R_stamp__) when the process with %(__pid__) crashed."
```

The tokens "`%(__host__)`", "%(`R_stamp__`)" and "%(`__pid__`)" are
references to other fields in the same event.

#### Other special attributes {#Otherspecialattributes}

There are couple other special attributes that ELAPI handles internally.

##### `R_stamp__` {#R_stamp__}

The value of this attribute is expected to be a format rather than a
value itself. The ELAPI will resolve the time stamp automatically and
insert it into the output without affecting the original event so that
it can be copied around and used as a base for another event.

##### `R_time__` {#R_time__}

The value of this attribute is ignored. It is automatically resolved
with the current UTC time (number of seconds since 1970).

##### `R_loco__` {#R_loco__}

The value of this attribute is ignored. It is automatically resolved
with the current offset between the local time UTC time (number of
seconds).

#### Event context {#Eventcontext}

Attributes that need special handling should be resolved once per event
submission but since event can be sent to different targets and sinks it
makes sense to resolve these attributes once and then carry them around
in a resolved event. Events are based on collection interface
([common/collection/collection.h](https://fedorahosted.org/sssd/browser/common/collection/collection.h){.source})
and support reference counts. thus one copy of immutable data (already
resolved event) can be used by different targets. When the event writing
is complete the destructor will be called against the event reference
and the count will be decreased. This way it does not matter which
target finishes logging first in the async case, the data will be around
for other targets to finish logging. The event will be completely
deleted when last target completes the task. There are other elements of
the event context that are important. They are discussed later.

### Event Template {#EventTemplate}

Sometimes it makes sense to create a common collection of attributes and
reuse then with different events. This is what the templates are for. A
template is a collection of the event attributes that are frequently or
always used. The "time stamp", "PID", "hostname" and some others are
good examples of such attributes. Combining them together once in a set
and reusing simplifies coding and optimizes performance since resolving
names and IP addresses might be costly. The developer can create,
destroy, modify and copy templates. It advised to create a set of the
templates at the initialization of the application and them just reuse
them. API allows creating events based on the templates or even logging
events right away by implicitly constructing event using template and
submitting it into the log dispatcher.

### Target {#Target}

#### Overview {#Overview2}

The concept of a "target" is introduced to separate logging destinations
logically and to allow one event be sent to different destinations at
the same time. ELAPI supports three default targets: "debug", "audit"
and "log". Other destinations can be added/defined by the developer of
the application that utilizes ELAPI. In this case a new section should
be added to the ELAPI configuration file. The target is a bit mask
argument specified by caller of the interface. The configuration file
shall contain targets with corresponding bit mask values. At run time
the bit masks provided by caller and bit mask provided in the
configuration file are compared. If logical AND of those is positive the
event will be sent to the specific target.

ELAPI defines three default targets using the following values:

-   debug is 1
-   audit is 2
-   log is 4

This mapping is really just a convention. The configuration file (see
details below) allows defining different targets (just names of the
sections in the file) and assigning them a number. It is really does no
matter how they are named but for convenience ELAPI provides three pre
configured targets mentioned above.

The log dispatcher tries all the targets listed in the configuration and
makes decision based on the result of the bit mask evaluation. As it was
said above target is a logical destination. Targets must be unique.
Specifying target twice will not rise error but only one target object
will be created by ELAPI. Each target has its own section in the
configuration file. This section specifies sinks (physical destinations)
that constitute the target and the bit mask "value" needed for
evaluation.

For more details see comments and examples in the
[common/elapi/elapi\_test/elapi\_ut.conf](https://fedorahosted.org/sssd/browser/common/elapi/elapi_test/elapi_ut.conf){.source}.

#### Internal Implementation {#InternalImplementation}

Internally target is treated as an object. This means that memory for it
is allocated and the main reference to a target object is a pointer to a
memory. The target has functions to create and destroy. Creating target
means allocating memory for its context and filling it. Destroying means
freeing the allocated memory that different parts of context use and
freeing the context itself. List of targets is implemented using
pointers to allocated context not the context data itself. So the data
stored in collection is a pointer. To simplify an explanation here is
the example. For simplicity let us assume that out context consists of
two integer variables.

``` {.wiki}
struct ctx 
{
    int a;
    int b;
}
```

The collection of targets could have been implemented in different ways.
It could save a copy of the context or a pointer to it. In first case it
will store a block of data with the contents of the context structure
(variables a and b), in the second case it will store just a pointer.
The collection of targets keeps pointers. This approach is preferable
since it reduces the number of memory allocation operations and data
duplication.

### Sink {#Sink}

#### Overview {#Overview3}

The sink describes a physical destination. Each target might consist
from more than one physical destination i.e. more than one sinks. Each
sink is associated with a specific logging facility (provider, see
below) like file, syslog, database, remote logging server etc. The sinks
specified for a target constitute a fail over chain. This means that
when the ELAPI tries to log into the "target" it will use first sink
from the list. If this sink fails to log the event then next sink will
be tried until all sinks are tried and logging either successes or
fails. The fail over and retry logic is a bit more complex than that.
One must also keep in mind that sinks usually (if implemented properly)
allow asynchronous operations so the failure might be resolved
internally. The error will be returned to caller only if all best
efforts (within given configured fail over and retry rules) failed.\
Each sink has its own section in the configuration file. This section
specifies settings related to a specific sink.

For more details see comments and examples in the
[common/elapi/elapi\_test/elapi\_ut.conf](https://fedorahosted.org/sssd/browser/common/elapi/elapi_test/elapi_ut.conf){.source}.
Same sink can be used for different targets in different places in the
fail over chain.

#### Internal Implementation {#InternalImplementation1}

Sinks, similarly to the targets, are implemented as objects and list of
sinks keeps references to the sink memory rather than a copy of the
sink's data. Internally dispatcher has list of sinks and list of
targets. Each target has an array of sinks it deals with. The data in
this array (implemented as dynamic array with reference count) is an
index of the sink in the global array of sinks constructed at the
creation of the dispatcher.

#### Sink Configuration {#SinkConfiguration}

There is a set of common parameters that are applicable to each sink.
For details see
[common/elapi/elapi\_test/elapi\_ut.conf](https://fedorahosted.org/sssd/browser/common/elapi/elapi_test/elapi_ut.conf){.source}.

### Providers {#Providers}

#### Overview {#Overview4}

Provider is the implementation of a "writer" functionality. Each sink is
logging via a provider. Two sinks can write via same provider. For
example there is a "file" provider. It is capable of taking and event,
serializing it and writing it into a file. There can be several sinks in
the configuration that take advantage of the same provider. For example
assume that there is a "log" target that consists of two sinks in the
fail over chain: "nfsfile" and "localfile". Both these sinks will write
to a file but these would be two different files. So in this case the
provider will be same for two different sinks. The sinks will differ in
configuration, they will use different file name, might have different
format or set of fields. There are a lot of parameters that can be
defined around each provider. All the provider specific configuration
parameters shall be listed in the same sink definition section of the
configuration file.

#### Implementation {#Implementation}

There are two embedded providers that ELAPI will provide out of box:
file and syslog.

##### File Provider {#FileProvider}

File provider configuration consists of two sets of parameters. First
set denotes parameters that are common for all formats supported by this
provider. The second set is the collection of groups of parameters where
each group is associated with a specific format. Internally a provider
is represented by a context object (a structure). This structure
contains information that provider needs to keep about itself during run
time. On of the parts of the context is the configuration structure.
This configuration structure holds the parameters common for all the
formats supported by provider. The format specific configuration is
stored in a separate structure pointer to which is stored in the
configuration structure. It is done this way to not have a huge
structure with all possible configuration parameters for all formats.
This would have been a waste of memory since only one format can be
configured at a time (well... actually two see below). Another reason to
keep format specific information separately from common parameters is
that there are two main very loosely coupled functions that a provider
(especially a "file" provider) should perform: serialize and write. The
code to serialize should not and does not care what happens with
serialized data while the part of code that actually writes the data
should not care about format. This situation creates a good argument for
separation of duties between two functions: serialize and write. As a
result the file provider reads common part of the configuration,
identifies the format and then calls a special format handler that would
read the format specific configuration. The file provider sees the
format specific data as opaque pointer and does not have a clue what
parameter the format handler cares about. When the event is submitted
into the sink and passed from sink to provider a special serialization
function is invoked by the provider. The opaque pointer with the format
specific configuration is passed into this function. The serialized data
is stored in a specific common for all providers structure and ready to
be sent into a file or socket.

##### Supported formats {#Supportedformats}

There is a plan to support the following formats:

1.  CSV
2.  HTML
3.  XML
4.  JSON
5.  Key value pairs
6.  Free format (might be extracted into a special provider)

The first implementation might not have all the formats supported. So
far CSV format is implemented.

##### [Append/Create?](https://docs.pagure.org/sssd-test2/Append/Create.html){.missing .wiki} logic {#AppendCreatelogic}

(To be implemented)

The configuration is read once when ELAPI is initialized. At that moment
all the sinks and provers are loaded and initialized. At the same time
the file specified as a destination for output is checked. If the file
is not present it is created. If the file is present the file will be
just opened. In both cases the launch marker will be added. The marker
is a configurable string that is used to identify the beginning of the
application run. After the marker format specific headers if any will be
inserted. Then if the file is configured to be kept open it will be kept
open. In this case the parameter that defines how frequently the
buffered data should be flushed to a file is respected. If the provider
is configured to open and close the file on each event it will do so and
then the flushing parameter is ignored since closing the file forces a
flush operation.

##### Configuration changes {#Configurationchanges}

(To be implemented)

One of the important things that one needs to keep in mind is that the
output file is treated as a continuous stream of data. It is never
rotated by the ELAPI. Use logrotate to rotate such files. However ELAPI
needs to deal with the cases when the configuration changes. For example
someone stopped application, set format to CSV, ran application, stopped
it, changed format again to HTML and started it again keeping the file
name same. The data will be sent to that file but in different formats.
The launch marker mentioned above becomes important. Also some formats
(like XML, HTML) require opening and closing tags at the beginning and
at the end so those tags will be inserted at the initialization and
finalization times respectfully.

##### Special stderr configuration {#Specialstderrconfiguration}

(To be implemented)

The "stderr" can be used as a special value for the name of the file. In
this case the file sink will use file descriptor 2 for its output. If
file descriptor 2 is not opened (for example it was closed during the
application initialization if application is a daemon) the provider will
return unrecoverable failure so such sink should not be configured as
required otherwise the ELAPI dispatcher will fail to start. There will
be no attempt at least in first implementation to reopen file descriptor
2 and connect back to terminal if descriptor 2 was deliberately closed
by the application.

##### Notion of sets {#Notionofsets}

Let us look at the following use case: my ELAPI application emits all
sorts of events that are created using different templates, but there is
really a common set of fields that I mostly care about, so I want the
output to have a predefined set of columns. If the key is missing in the
event I want the output to contain an empty value. To accomplish this I
can define a set of fields in the configuration file and this set of
fields will always constitute my output. But what about other fields
that are not a part of the set but may be a part of the event? I might
want to have them in the output too but only as additional fields after
the predefined set. For some formats having "leftovers" be presented as
separate columns or fields in the output might be preferable but there
are formats for which it makes sense to jam the leftovers together in
one field. When one defines a set in the configuration file for a sink a
special string "@" can be put at the end of the set. It would denote
that all the leftovers need to be added to the end of the output as
separate fields. The string "@n" will specify that the leftovers need to
be jammed into one format and this format number is specified by "n".
The internal implementation parses the event and splits it in two parts:
the fields predefined by the set and leftovers. Then depending upon the
configuration the fields are serialized and the output is constructed.

### ELAPI Configuration {#ELAPIConfiguration}

The example of the ELAPI configuration file with comments can be found
here
[common/elapi/elapi\_test/elapi\_ut.conf](https://fedorahosted.org/sssd/browser/common/elapi/elapi_test/elapi_ut.conf){.source}.
The application initializing ELAPI needs to call initialization
function. There are couple different initialization functions that can
be used depending upon the type of the application see details below and
in the
[common/elapi/elapi\_log.h](https://fedorahosted.org/sssd/browser/common/elapi/elapi_log.h){.source}.
One of the arguments to those functions is the name of the application
(appname) and another is a path to configuration file or directory
(config\_path). The following logic is used to determine where and how
to read the ELAPI configuration for the application:

``` {.wiki}
   If config_path = NULL the configuration will be read from the standard locations:
    - First from the global configuration file "elapi.conf" located in the directory
      defined at the compile time by the ELAPI_DEFAULT_CONFIG_DIR constant.
      This file is assumed to contain common ELAPI configuration for this host;
    - Second from the file with name constructed from appname by appending to it
      suffix ".conf". The file will be looked in the directory pointed by
      ELAPI_DEFAULT_CONFIG_APP_DIR constant that is defined at compile time.
    The data from second file overwrites and complements the data from the first
    one.
    It is expected that applications will take advantage of the common
    central convention so config_path should be NULL in most cases.
  
   If config_path points to a file the function will try to read the file
   as if it is a configuration file. The appname is ignored in this case.
   If config_path points to a directory, the function will try to read
   configuration from the file with name constructed by appending suffix ".conf"
   to appname. The file will be looked up in that directory.
   If the config_path is neither file or directory the default values will be used
   to initialize dispatcher.
```

### Dispatcher {#Dispatcher}

Dispatcher is the core of the ELAPI logic. It is the collection of
targets and sinks. It keeps track of sink statuses and checks where the
event should be sent. Application can instantiate multiple dispatchers
with different configurations. This is useful for the thread
applications. In such cases it is important to use only re-entrant
sinks. Syslog sink is not re-entrant sink so it should be used with
caution. It is recommended to phase out use of the syslog sink as soon
as possible to avoid issues with its inability to act properly in
re-entrant environments.

### Sync vs Async {#SyncvsAsync}

Internally the ELAPI is written as the asynchronous interface. However
the use of the synchronous or asynchronous interface should be
correlated to the way the dispatcher is initialized. The low level
dispatcher initialization call looks like this (see
[common/elapi/elapi\_test/elapi\_dispatcher.h](https://fedorahosted.org/sssd/browser/common/elapi/elapi_test/elapi_dispatcher.h){.source}
for more details):

``` {.wiki}
int elapi_create_dispatcher(struct elapi_dispatcher **dispatcher,  /* Handle of the dispatcher will be stored in this variable */
                            const char *appname,                   /* Application name. Passed to the sinks to do initialization */
                            const char *config_path,               /* See notes below in the elapi_init() function. */
                            struct elapi_async_ctx *ctx);          /* Async context. If NULL internal context will be used */
```

The use of the async or synch API with a dispatcher depends upon what is
specified in the last parameter of the call. If the application is using
its own async loop it can construct the async context object using
provided API and pass it to the elapi\_create\_dispatcher() function.
The async context object is a set of the callbacks and pointers to data
that application wants to pass to those callbacks. The callbacks are
used by ELAPI when ELAPI wants to request read or write operation on a
file descriptor or wants to create a timer. If the application provides
its callbacks the ELAPI will be fully integrated into the main event
loop of the application. It will process submitted log events
asynchronously and will call application provided callback at different
points of processing (depending upon passed in flags). If application
calls synch API it will wrap the internal async calls and will not
return until the events are logged. This is accomplished by internally
looping using loop\_once() callback provided by application as part of
the async context object.\
If the application calls dispatcher and does not provide the async
context the dispatcher will be initialized internally using internal
loop. So if the synch API is called the ELAPI will use the internal loop
to process the event. If the async API is called the caller would have
to provide a callback that will be invoked at the special moments of the
event processing. The async call will return right away and the caller
would have to get back to checking the results of the invocation when
all necessary callbacks are executed. The synch API does exactly that so
there is no sense to use async API with a dispatcher that is not
integrated with the application loop.

### Walk Through the Dispatcher Creation Call {#WalkThroughtheDispatcherCreationCall}

-   Validate input
-   Allocate memory for dispatcher data
-   Read configuration file
-   Initialize global internal objects like hash table and list of
    resolvers
-   Build target lists and sink chains. As a part of this operation:
    **The list of targets is created** Then the list of sinks is
    created. **The sink arrays are constructed for each target denoting
    the fail over chains. The sink array contains the index of the sink
    in the global list of sink stored in dispatcher.** The providers are
    loaded and initialized for each sink
-   Initialize internal loop if the external loop data is not provided

### Walk Through the Synchronized Logging Call {#WalkThroughtheSynchronizedLoggingCall}

-   Create an error object. The error object contains an aggregated
    error state and collection of statutes related to each target the
    event was sent to.
-   Call async logging call. The call schedules the logging operation
    and returns. The details of what happens inside the async call are
    described below.
-   The loop\_once() callback is executed until the error object gets
    into the "done" state. After this the call returns to the caller.

### Walk Through the Asynchronous Logging Call {#WalkThroughtheAsynchronousLoggingCall}

-   The event is resolved. As a result a new "resolved" event where the
    values for all special keys are resolved.
-   The tracker object is created. The tracker object is the internal
    ELAPI object that tracks how many instances of the event are being
    loged into different targets at the same time.
-   The event is sent into the target list. This is when the target list
    is traversed and for each matched target the event context object is
    created. The event context object attaches to the tracker. The
    tracker records how many event contexts are expected and how many
    event context are actually created. When the processing of the event
    failed early and the event context was not created there will be
    less event contexts tracked than tracker expects. The whole point of
    ELAPI is to try to log as much as possible even if logging into some
    of the targets failed. Tracker object helps with this goal. It
    compares number of expected event contexts to the actual number of
    event context and makes sure that the caller does not wait for the
    completion of the logging of the event when the event context
    creation already failed. The event context object keeps reference to
    the resolved event, target's sink array and other target related
    properties. At this stage the event starts its journey through the
    callback chain.
-   The callback chain for each event context object consist of the
    sequence of operations executed by one high level processing
    callback function. This is the function that looks at the event
    context, determines its state and does an operation it is supposed
    to do in this state. Then it schedules execution of the itself again
    passing in the event context. When time comes the function is called
    again but now the event is in a different state so different
    operation is performed. The list of operations includes doing a
    logging operation via interrogating with the sink object or calling
    a user provided callback in a specific state. Think about this
    function being a rocket in the table tennis when someone just
    juggles the ball (event context) on the rocket. Just imagine that
    every time the ball hits the rocket the internal reaction happens
    and the ball changes its color. Same here, the ball i.e. the event
    context goes through the chain of states and finally gets destroyed
    when the event is successfully logged, operation failed or was
    canceled by application via callback return code. One of the states
    is interrogating with sink. What is done in this state depends upon
    the state of the sink. The sink can be active so the event will be
    scheduled for logging. As soon as the file descriptor is ready for
    writing the event will be written into the file descriptor. The sink
    can be suspended, then depending upon the configuration the sink
    might be skipped or the ELAPI might decide that it is time to revive
    the sink. If the logging into the sink fails the event context will
    be scheduled to start over with next sink in the chain.
-   When the async logging call is executed the caller needs to provide
    the callback and a "flags" argument. The flags argument determines
    in which state(s) the application provided callback needs to be
    executed. By default the callback will be executed when the
    processing of the sink chain ends due to error or success and when
    all the copies of the same event destined for different targets
    complete their journey.

### Module List {#ModuleList}

-   **elapi\_dispatcher.c** - code to create and destroy dispatcher
-   **elapi\_dispatcher.h** - interface definition for dispatcher
    related operations. This interface is external.
-   **elapi\_log.c** - code to log the event synchronously or
    asynchronously
-   **elapi\_log.h** - interface to log the event synchronously or
    asynchronously. This interface is external.
-   **elapi\_event.c** - code to construct events and templates from
    key-value pairs and collections
-   **elapi\_event.h** - interface to the event creation functions. This
    interface is external.
-   **elapi\_ioctl.c** - specific code to populate the network related
    attributes
-   **elapi\_ioctl.h** - header for specific code to populate the
    network related attributes
-   **elapi\_net.h** - header for specific code to populate the network
    related attributes
-   **elapi\_resolve.c** - code to resolve the elements of the event
-   **elapi\_subst.c** - code to perform substitution used in resolution
    code
-   **elapi\_error.c** - code to implement error and status object. Used
    by synch code to keep track of the aggregated result.
-   **elapi\_error.h** - interface to the event object. This interface
    is external. It consists of two parts. One for processing results
    after the synch call returns to caller and another for building of
    the synch wrappers.
-   **elapi\_loop.c** - code to implement internal event loop.
-   **elapi\_loop.h** - intern event loop callbacks. This interface is
    external.
-   **elapi\_async.c** - code to create the object that has all the
    async callbacks
-   **elapi\_async.h** - interface to the async object. This interface
    is external.
-   **elapi\_target.c** - code to implement target object.
-   **elapi\_target.h** - interface to the target object. This interface
    is internal.
-   **elapi\_sink.c** - code to implement sink object.
-   **elapi\_sink.h** - interface to the sink object. This interface is
    internal.
-   **elapi\_evctx.c** - code to implement event context object
-   **elapi\_evctx.h** - interface to the event context object. This
    interface is internal.
-   **elapi\_tracker.c** - code to implement tracker object
-   **elapi\_tracker.h** - interface to the tracker object. This
    interface is internal.
-   **elapi\_priv.h** - the main internal ELAPI header file that defines
    all the internal data
-   **elapi\_plugin.h** - the internal ELAPI header file that defines
    the provider interface
-   **elapi\_defines.h** - some of the ELAPI constants
-   **elapi.h** - high level header that includes all public interfaces
    exposed by ELAPI
-   **elapi\_basic.c** - the basic object for data serialization
-   **elapi\_basic.h** - interface to the basic data serialization
    object. This interface is internal but supposed to be used by the
    providers.

