<div class="wiki-toc">

1.  1.  [SSSD - System Security Services
        Daemon](#SSSD-SystemSecurityServicesDaemon)
        1.  [Resources](#Resources)
        2.  [Releases](#Releases)
        3.  [Social Networking](#SocialNetworking)

</div>

SSSD - System Security Services Daemon {#SSSD-SystemSecurityServicesDaemon}
--------------------------------------

SSSD is a system daemon. Its primary function is to provide access to
identity and authentication remote resource through a common framework
that can provide caching and offline support to the system. It provides
PAM and NSS modules, and in the future will D-BUS based interfaces for
extended user information. It provides also a better database to store
local users as well as extended user data.

Documentation on configuring SSSD in Fedora or Red Hat Enterprise Linux
is available from [[​]{.icon}the RHEL deployment
guide](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html-single/Deployment_Guide/index.html#SSSD-Introduction){.ext-link}.
We also have a dedicated [Documentation
section](https://docs.pagure.org/sssd-test2/Documentation.html){.wiki}

Having problems? Check out our [troubleshooting
page](https://docs.pagure.org/sssd-test2/Troubleshooting.html){.wiki} or
the "[Frequently Asked
Questions](https://docs.pagure.org/sssd-test2/FAQ.html){.wiki}" page for
answers to common issues.

If you would like to contribute to the SSSD, a good place to start would
be our
[Contributions](https://docs.pagure.org/sssd-test2/Contribute.html){.wiki}
page.

If you want to file a bug or enhancement request, please log in with
your Fedora Account System credentials. If you do not have a Fedora
Account, you can register for one at
[[​]{.icon}https://admin.fedoraproject.org/accounts/](https://admin.fedoraproject.org/accounts/){.ext-link}

### Resources {#Resources}

-   [Design
    Documents](https://docs.pagure.org/sssd-test2/DesignDocs.html){.wiki}
-   [Documentation and
    HOWTOs](https://docs.pagure.org/sssd-test2/Documentation.html){.wiki}
-   [Developer
    Information](https://docs.pagure.org/sssd-test2/DevRes.html){.wiki}
-   [Configuring sssd to authenticate with a Windows
    Server](https://docs.pagure.org/sssd-test2/Configuring_sssd_with_ad_server.html){.wiki}

### Releases {#Releases}

Latest Stable Release:

  ------------------------------------------------------------------------------------------------------ -------------------------------------------------------------------------------------------------------------- ------------------------------------------------------ --------------------------------------------------------------------------------------- -----------------------------------------------------------------------------------
  [[​]{.icon}sssd-1.15.0.tar.gz](https://releases.pagure.org/sssd-test2/sssd-1.15.0.tar.gz){.ext-link}   [[​]{.icon}sssd-1.15.0.tar.gz.asc](https://releases.pagure.org/sssd-test2/sssd-1.15.0.tar.gz.asc){.ext-link}   SHA1SUM: `0c9fc62c1b9bcdca649223d9f673b9a73f273e56`\   Date: 2017-01-25\                                                                       [[​]{.icon}Manpages](http://jhrozek.fedorapeople.org/sssd/1.15.0/man/){.ext-link}
                                                                                                                                                                                                                        MD5SUM: `0c151a045e5292fece1e991b665d525c`             [Release Notes](https://docs.pagure.org/sssd-test2/Releases/Notes-1.15.0.html){.wiki}   
  ------------------------------------------------------------------------------------------------------ -------------------------------------------------------------------------------------------------------------- ------------------------------------------------------ --------------------------------------------------------------------------------------- -----------------------------------------------------------------------------------

Latest LTM Release:

  ------------------------------------------------------------------------------------------------------ -------------------------------------------------------------------------------------------------------------- ------------------------------------------------------ --------------------------------------------------------------------------------------- -----------------------------------------------------------------------------------
  [[​]{.icon}sssd-1.13.4.tar.gz](https://releases.pagure.org/sssd-test2/sssd-1.13.4.tar.gz){.ext-link}   [[​]{.icon}sssd-1.13.4.tar.gz.asc](https://releases.pagure.org/sssd-test2/sssd-1.13.4.tar.gz.asc){.ext-link}   SHA1SUM: `8332501d752ab82f994170d11d31d5d15912b2e9`\   Date: 2016-04-13\                                                                       [[​]{.icon}Manpages](http://jhrozek.fedorapeople.org/sssd/1.13.4/man/){.ext-link}
                                                                                                                                                                                                                        MD5SUM: `d147e0a4f4719d993693c6a99370b350`             [Release Notes](https://docs.pagure.org/sssd-test2/Releases/Notes-1.13.4.html){.wiki}   
  ------------------------------------------------------------------------------------------------------ -------------------------------------------------------------------------------------------------------------- ------------------------------------------------------ --------------------------------------------------------------------------------------- -----------------------------------------------------------------------------------

Previous LTM Release:

  ---------------------------------------------------------------------------------------------------- ------------------------------------------------------------------------------------------------------------ ------------------------------------------------------ -------------------------------------------------------------------------------------- ----------------------------------------------------------------------------------
  [[​]{.icon}sssd-1.9.7.tar.gz](https://releases.pagure.org/sssd-test2/sssd-1.9.7.tar.gz){.ext-link}   [[​]{.icon}sssd-1.9.7.tar.gz.asc](https://releases.pagure.org/sssd-test2/sssd-1.9.7.tar.gz.asc){.ext-link}   SHA1SUM: `941c5f479664a50a8611a4d1bcec7226f25f7add`\   Date: 2014-12-05\                                                                      [[​]{.icon}Manpages](http://jhrozek.fedorapeople.org/sssd/1.9.7/man/){.ext-link}
                                                                                                                                                                                                                    MD5SUM: `d35149f567a7c158715b55c93c8d91cb`             [Release Notes](https://docs.pagure.org/sssd-test2/Releases/Notes-1.9.7.html){.wiki}   
  ---------------------------------------------------------------------------------------------------- ------------------------------------------------------------------------------------------------------------ ------------------------------------------------------ -------------------------------------------------------------------------------------- ----------------------------------------------------------------------------------

Latest Stable Release of DING-LIBS

  ------------------------------------------------------------------------------------------------------------------- --------------------------------------------------------------------------------------------------------------------------- ------------------------------------------------------ ------------------------------------------------------------------------------------------
  [[​]{.icon}ding-libs-0.6.0.tar.gz](https://fedorahosted.org/released/ding-libs/ding-libs-0.6.0.tar.gz){.ext-link}   [[​]{.icon}ding-libs-0.6.0.tar.gz.asc](https://fedorahosted.org/released/ding-libs/ding-libs-0.6.0.tar.gz.asc){.ext-link}   SHA1SUM: `c8ec86cb93a26e013a13b12a7b0b3fbc1bca16c1`\   Date: 2016-06-22\
                                                                                                                                                                                                                                                  MD5SUM: `0dd0a95f2f8d65b84d3cb9568494109a`             [Release Notes](https://docs.pagure.org/sssd-test2/Releases/DingNotes-0.6.0.html){.wiki}
  ------------------------------------------------------------------------------------------------------------------- --------------------------------------------------------------------------------------------------------------------------- ------------------------------------------------------ ------------------------------------------------------------------------------------------

Older releases are available on our
[Releases](https://docs.pagure.org/sssd-test2/Releases.html){.wiki}
page.

### Social Networking {#SocialNetworking}

[Follow @SysSecSvcDaemon on
Twitter!](http://twitter.com/SysSecSvcDaemon){.twitter-follow-button}

Join the [[​]{.icon}SSSD
Google+](https://plus.google.com/114204339376082660377){.ext-link} page
