Procedure for updating empty-\* packages
========================================

Background
----------

The `empty-*` packages were introduced a workaround for sites that install certain software (for example HTCondor or CA certs) from tarballs or other means that do not involve Yum/RPM.

The packages contain no files, and exist merely to satisfy RPM dependencies so that other packages can be installed. It is the admin's responsibility to make sure that whatever component they installed the empty package for is functional.

The empty packages are kept in a separate repository to prevent them from being accidentally installed instead of the component they claim to provide. Because of this, they do not go through the normal release process of development to testing to prerelease to release, but are *moved* straight from `osg-development` into `osg-empty` after developer testing. 

!!! warning
    It is important to untag the packages from `osg-development` immediately after promotion to `osg-empty`

Procedure
---------

1.  Prepare the package update, but do not build yet.
2.  Coordinate with the Software and Release Managers to set aside a good time to update the package. An empty package should not remain in the development repos for longer than a few hours.
3.  Build into development.
4.  Test out of development. *Be thorough*, as there is no separate acceptance testing for empty packages.
5.  In the JIRA ticket, document your testing procedure and request permission from *both* the Software and the Release Managers. (Since there is no acceptance testing, both of them have to sign off on the new build).
6.  After receiving permission, tag the builds into the `osg-empty` tags, and untag them from the `osg-development` tags. Then regenerate the `osg-empty` repos. <pre class="screen">

```
osg-koji move-pkg osg-3.3-el6-development osg-3.3-el6-empty <EL6_BUILD_NVR>
osg-koji move-pkg osg-3.3-el7-development osg-3.3-el7-empty <EL7_BUILD_NVR>
osg-koji regen-repo --nowait osg-3.3-el6-empty
osg-koji regen-repo --nowait osg-3.3-el7-empty
```
