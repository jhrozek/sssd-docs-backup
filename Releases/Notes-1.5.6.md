<div class="wiki-toc">

1.  1.  [Highlights](#Highlights)
    2.  [Detailed Changelog](#DetailedChangelog)

</div>

Highlights {#Highlights}
----------

-   Fixed a serious memory leak in the memberOf plugin
-   Fixed a regression with the negative cache that caused it to be
    essentially nonfunctional
-   Fixed an issue where the user's full name would sometimes be removed
    from the cache
-   Fixed an issue with password changes in the kerberos provider not
    working with kpasswd

Detailed Changelog {#DetailedChangelog}
------------------

Simo Sorce (2):

-   memberof: fix calculation of replaced members
-   memberof: free delete operation payload once done

Stephen Gallagher (7):

-   Never remove gecos from the sysdb cache
-   Do not throw a DP error when failing to delete a nonexistent entity
-   Add debug logging to the negative cache
-   Fix a regression with the negative cache in multi-domain
    configurations
-   Fix regression where nonexistent entries were never added to the
    negative cache
-   Bumping version to 1.5.6
-   Always generate kpasswdinfo file

