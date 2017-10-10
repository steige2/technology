Old Release Series Removal Plan
===============================

In order to reduce clutter and disk usage on our repositories and build system,
we will remove older OSG Software release series.  This will result in packages
from those series becoming unavailable, so we will remove a release series when
its packages are no longer needed.

We will remove a release series when the _following_ series is completely out
of support.  For example, OSG 3.1 will be removed when OSG 3.2 is out of
support, and OSG 3.2 will be removed when OSG 3.3 is out of support.


Tasks
-----

Removing a release series requires work from Software & Release, and
coordination with Operations. The first step is to create a JIRA ticket
in the SOFTWARE project to track the work.

Tasks in the 'Repo Update' section need to be completed before tasks in
the 'Software 'Update' section; also, tasks in the 'Repo Update' section
require coordination with Operations.


### Repo Update

These tasks should be completed in order.

1.  Two weeks in advance, Operations should notify sites (including mirror
    sites) that the release series is going away.

2.  Software & Release should ask permission from Operations to do
    the following removal tasks on repo-itb.grid.iu.edu.
    
3.  Remove the series from the mash configs.

4.  Remove the appropriate mirrorlist directories from `/usr/local/mirror/osg`.

5.  Remove the appropriate repo directories from `/usr/local/repo/osg`.

6.  Wait for mash to run and verify that the repos are no longer getting
    updated:

    -  Look at the mash logs in `/var/log/repo`.
    -  Verify that mash did not recreate the repo directory under
       `/usr/local/repo/osg` corresponding to the old release series.

7.  Software & Release should ask permission from Operations to do
    these same removal tasks on repo1.grid.iu.edu and repo2.grid.iu.edu.

### Software Update

These tasks can be completed in any order.

- Tag and remove the SVN branch corresponding to the release series.

- Edit `vm-test-runs` and remove any "long tail" tests that reference the
  series.

- Edit `tarball-client`:

  - Remove bundles from `bundles.ini`.
  - Remove patch and other files that were used only by those bundles.
  - Test that the current bundles didn't get broken by your changes.

- Edit `osg-build`:

  - Remove the promotion routes from `promoter.ini`.
  - Remove references in `constants.py`.
  - Test your changes; also run the unit tests.

- Remove things from Koji:

  - All targets referencing the series.
  - All tags referencing the series.

- Remove references to the series from `opensciencegrid/docker-osg-wn-scripts`
  on GitHub, including the `genbranches` and `update-all` scripts.

- Remove branches from `opensciencegrid/docker-osg-wn` on GitHub.

- Move files in `/p/vdt/public/html/release-info` to its `attic` subdirectory.


Undoing
-------

If we really need RPMs from a removed release series, we can look at the text
files in `/p/vdt/public/html/release-info/attic` to determine the exact NVRs we
need, and download them from Koji.

