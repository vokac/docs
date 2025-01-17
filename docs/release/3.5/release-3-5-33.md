!!! failure "OSG 3.5 end-of-life"
    The OSG 3.5 end-of-life date was May 1, 2022 per our
    [release policy](https://osg-htc.org/technology/policy/release-series/).
    We recommend
    [updating to OSG 3.6](../updating-to-osg-36.md)
    at your earliest convenience.

title: OSG 3.5.33

OSG Software Release 3.5.33
===========================

**Release Date:** 2021-04-01  
**Supported OS Versions:** EL7, EL8

!!!tip "Want faster access to production-ready software?"
    OSG 3.5 offers a rolling release repository where packages are added as soon as they pass acceptance testing.
    To install packages from this repository, enable `[osg-rolling]` in `/etc/yum.repos.d/osg-rolling.repo`:

        [osg-rolling]
        ...
        enabled=1

    Or for one-time installations, append the following to your `yum` command:

        --enablerepo=osg-rolling

Summary of Changes
------------------

!!! bug "Known issues with XRootD 5.1.1"
    -   The XRootD team is [evaluating solutions for a memory leak](https://github.com/xrootd/xrootd/pull/1431) in the
        HTTP Third-Party Copy (HTTP-TPC) use case related to `libcurl` and `NSS`.
        These leaks appear to exist in `libcurl` for all versions of XRootD and their impact depends on the transfer
        load at each site.
    -   [Incompatibility with the multi-user plugin](https://github.com/opensciencegrid/xrootd-multiuser/issues/21):
        users of the XRootD multi-user plugin will be unable to update to XRootD 5.1.x until a fixed version
        of XRootD multi-user is released into the OSG repositories
    -   In some cases, XCaches using the Rucio plug-in may crash due to malformed URLs generated by the plug-in.

This release contains the following changes to the `osg-upcoming` repository:

-   **XRootD 5.1.1** (EL7 only): an update from the previously available version, XRootD 5.0.2
    -  See [this section](../updating-to-osg-35.md#updating-to-xrootd-5) for detailed update instructions
    -  The XRootD SciTokens plug-in (`xrootd-scitokens`) has been merged into the XRootD code-base so its version now matches the `xrootd`
       package version
    -  See the [upstream release notes](https://github.com/xrootd/xrootd/blob/v5.1.1/docs/ReleaseNotes.txt#L9-L164) for
       details
-   **XCache 2.0.0**
    -  Updated configuration for XRootD 5.1 compatible chaining of authorization libraries
       ([SOFTWARE-4431](https://opensciencegrid.atlassian.net/browse/SOFTWARE-4431))
    -  Added requirement for XRootD 5.1
       ([SOFTWARE-4431](https://opensciencegrid.atlassian.net/browse/SOFTWARE-4431))
-   **XRootD HDFS 2.2.0**
    -   Fixed a bug where checksums were written on HDFS write failures, potentially confusing clients
        ([#34](https://github.com/opensciencegrid/xrootd-hdfs/pull/34))
    -   Added support for new extended attribute API, allowing token plugins to properly set the username needed by HDFS
        ([#35](https://github.com/opensciencegrid/xrootd-hdfs/pull/35))
-   **XRootD CMS TFC 1.5.2-6**: rebuilt against XRootD 5.1.1
-   **XRootD Rucio plug-in 1.2-3.3**: rebuilt against XRootD 5.1.1

These
[JIRA tickets](https://opensciencegrid.atlassian.net/issues/?jql=project%20%3D%20SOFTWARE%20AND%20fixVersion%20in%20(3.5.33%2C3.5.33-upcoming)%20ORDER%20BY%20priority%20DESC%2C%20key%20DESC)
were addressed in this release.

Containers
----------

The following container images have been updated to contain the new packages listed above:

-   `opensciencegrid/atlas-xcache:release`
-   `opensciencegrid/cms-xcache:release`
-   `opensciencegrid/stash-cache:release`
-   `opensciencegrid/stash-origin:release`
-   `opensciencegrid/xrootd-standalone:release`

Updating to the New Release
---------------------------

To update to the OSG 3.5 series, please consult the page on
[updating between release series](../updating-to-osg-35.md).

Need Help?
----------

Do you need help with this release? [Contact us for help](../../common/help.md).

Detailed Changes in This Release
--------------------------------

### Upcoming Packages

We added or updated the following packages to the **upcoming** OSG Yum repository.
Note that in some cases, there are multiple RPMs for each package.
You can click on any given package to see the set of RPMs or see the complete list below.

#### Enterprise Linux 7

-   [xcache-2.0.0-1.osgup.el7](https://koji.chtc.wisc.edu/koji/search?match=glob&type=build&terms=xcache-2.0.0-1.osgup.el7)
-   [xrootd-5.1.1-1.3.osg35up.el7](https://koji.chtc.wisc.edu/koji/search?match=glob&type=build&terms=xrootd-5.1.1-1.3.osg35up.el7)
-   [xrootd-cmstfc-1.5.2-6.osg35up.el7](https://koji.chtc.wisc.edu/koji/search?match=glob&type=build&terms=xrootd-cmstfc-1.5.2-6.osg35up.el7)
-   [xrootd-hdfs-2.2.0-1.osg35up.el7](https://koji.chtc.wisc.edu/koji/search?match=glob&type=build&terms=xrootd-hdfs-2.2.0-1.osg35up.el7)
-   [xrootd-rucioN2N-for-Xcache-1.2-3.3.osg35up.el7](https://koji.chtc.wisc.edu/koji/search?match=glob&type=build&terms=xrootd-rucioN2N-for-Xcache-1.2-3.3.osg35up.el7)

### Upcoming RPMs

If you wish to manually update your system, you can run yum update against the following packages:

    atlas-xcache cms-xcache python2-xrootd python36-xrootd Signatures: stash-cache stash-origin xcache xcache-consistency-check xcache-redirector xrootd xrootd-client xrootd-client-compat xrootd-client-devel xrootd-client-libs xrootd-cmstfc xrootd-cmstfc-debuginfo xrootd-cmstfc-devel xrootd-debuginfo xrootd-devel xrootd-doc xrootd-fuse xrootd-hdfs xrootd-hdfs-debuginfo xrootd-hdfs-devel xrootd-libs xrootd-private-devel xrootd-rucioN2N-for-Xcache xrootd-rucioN2N-for-Xcache-debuginfo xrootd-scitokens xrootd-selinux xrootd-server xrootd-server-compat xrootd-server-devel xrootd-server-libs xrootd-voms

If you wish to only update the RPMs that changed, the set of RPMs is:

#### Enterprise Linux 7

``` file
atlas-xcache-2.0.0-1.osgup.el7
cms-xcache-2.0.0-1.osgup.el7
python2-xrootd-5.1.1-1.3.osg35up.el7
python36-xrootd-5.1.1-1.3.osg35up.el7
stash-cache-2.0.0-1.osgup.el7
stash-origin-2.0.0-1.osgup.el7
xcache-2.0.0-1.osgup.el7
xcache-consistency-check-2.0.0-1.osgup.el7
xcache-redirector-2.0.0-1.osgup.el7
xrootd-5.1.1-1.3.osg35up.el7
xrootd-client-5.1.1-1.3.osg35up.el7
xrootd-client-compat-5.1.1-1.3.osg35up.el7
xrootd-client-devel-5.1.1-1.3.osg35up.el7
xrootd-client-libs-5.1.1-1.3.osg35up.el7
xrootd-cmstfc-1.5.2-6.osg35up.el7
xrootd-cmstfc-debuginfo-1.5.2-6.osg35up.el7
xrootd-cmstfc-devel-1.5.2-6.osg35up.el7
xrootd-debuginfo-5.1.1-1.3.osg35up.el7
xrootd-devel-5.1.1-1.3.osg35up.el7
xrootd-doc-5.1.1-1.3.osg35up.el7
xrootd-fuse-5.1.1-1.3.osg35up.el7
xrootd-hdfs-2.2.0-1.osg35up.el7
xrootd-hdfs-debuginfo-2.2.0-1.osg35up.el7
xrootd-hdfs-devel-2.2.0-1.osg35up.el7
xrootd-libs-5.1.1-1.3.osg35up.el7
xrootd-private-devel-5.1.1-1.3.osg35up.el7
xrootd-rucioN2N-for-Xcache-1.2-3.3.osg35up.el7
xrootd-rucioN2N-for-Xcache-debuginfo-1.2-3.3.osg35up.el7
xrootd-scitokens-5.1.1-1.3.osg35up.el7
xrootd-selinux-5.1.1-1.3.osg35up.el7
xrootd-server-5.1.1-1.3.osg35up.el7
xrootd-server-compat-5.1.1-1.3.osg35up.el7
xrootd-server-devel-5.1.1-1.3.osg35up.el7
xrootd-server-libs-5.1.1-1.3.osg35up.el7
xrootd-voms-5.1.1-1.3.osg35up.el7
```
