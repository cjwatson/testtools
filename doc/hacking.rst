=========================
Contributing to testtools
=========================

Coding style
------------

In general, follow `PEP 8`_ except where consistency with the standard
library's unittest_ module would suggest otherwise.

testtools supports Python 2.4 and later, including Python 3, so avoid any
2.5-only features like the ``with`` statement.


Copyright assignment
--------------------

Part of testtools raison d'etre is to provide Python with improvements to the
testing code it ships. For that reason we require all contributions (that are
non-trivial) to meet one of the following rules:

* be inapplicable for inclusion in Python.
* be able to be included in Python without further contact with the contributor.
* be copyright assigned to Jonathan M. Lange.

Please pick one of these and specify it when contributing code to testtools.


Licensing
---------

All code that is not copyright assigned to Jonathan M. Lange (see Copyright
Assignment above) needs to be licensed under the `MIT license`_ that testtools
uses, so that testtools can ship it.


Testing
-------

Please write tests for every feature.  This project ought to be a model
example of well-tested Python code!

Take particular care to make sure the *intent* of each test is clear.

You can run tests with ``make check``.


Documentation
-------------

Documents are written using the Sphinx_ variant of reStructuredText_.  All
public methods, functions, classes and modules must have API documentation.
When changing code, be sure to check the API documentation to see if it could
be improved.  Before submitting changes to trunk, look over them and see if
the manuals ought to be updated.


Source layout
-------------

The top-level directory contains the ``testtools/`` package directory, and
miscellaneous files like ``README`` and ``setup.py``.

The ``testtools/`` directory is the Python package itself.  It is separated
into submodules for internal clarity, but all public APIs should be “promoted”
into the top-level package by importing them in ``testtools/__init__.py``.
Users of testtools should never import a submodule in order to use a stable
API.  Unstable APIs like ``testtools.matchers`` and
``testtools.deferredruntest`` should be exported as submodules.

Tests belong in ``testtools/tests/``.


Commiting to trunk
------------------

Testtools is maintained using bzr, with its trunk at lp:testtools. This gives
every contributor the ability to commit their work to their own branches.
However permission must be granted to allow contributors to commit to the trunk
branch.

Commit access to trunk is obtained by joining the testtools-devs Launchpad
team. Membership in this team is contingent on obeying the testtools
contribution policy, including assigning copyright of all the work one creates
and places in trunk to Jonathan Lange.


Code Review
-----------

All code must be reviewed before landing on trunk. The process is to create a
branch in launchpad, and submit it for merging to lp:testtools. It will then
be reviewed before it can be merged to trunk. It will be reviewed by someone:

* not the author
* a committer (member of the `~testtools-dev`_ team)

As a special exception, while the testtools committers team is small and prone
to blocking, a merge request from a committer that has not been reviewed after
24 hours may be merged by that committer. When the team is larger this policy
will be revisited.

Code reviewers should look for the quality of what is being submitted,
including conformance with this HACKING file.

Changes which all users should be made aware of should be documented in NEWS.


NEWS management
---------------

The file NEWS is structured as a sorted list of releases. Each release can have
a free form description and more or more sections with bullet point items.
Sections in use today are 'Improvements' and 'Changes'. To ease merging between
branches, the bullet points are kept alphabetically sorted. The release NEXT is
permanently present at the top of the list.


Release tasks
-------------

#. Choose a version number, say X.Y.Z
#. Branch from trunk to testtools-X.Y.Z
#. In testtools-X.Y.Z, ensure __init__ has version ``(X, Y, Z, 'final', 0)``
#. Replace NEXT in NEWS with the version number X.Y.Z, adjusting the reST.
#. Possibly write a blurb into NEWS.
#. Replace any additional references to NEXT with the version being
   released. (should be none).
#. Commit the changes.
#. Tag the release, bzr tag testtools-X.Y.Z
#. Create a source distribution and upload to pypi ('make release').
#. Make sure all "Fix committed" bugs are in the 'next' milestone on
   Launchpad
#. Rename the 'next' milestone on Launchpad to 'X.Y.Z'
#. Create a release on the newly-renamed 'X.Y.Z' milestone

   * Make the milestone inactive (this is the default)
   * Set the release date to the current day

#. Upload the tarball and asc file to Launchpad
#. Merge the release branch testtools-X.Y.Z into trunk. Before the commit,
   add a NEXT heading to the top of NEWS and bump the version in __init__.py.
   Push trunk to Launchpad
#. If a new series has been created (e.g. 0.10.0), make the series on Launchpad.
#. Make a new milestone for the *next release*.

   #. During release we rename NEXT to $version.
   #. We call new milestones NEXT.

#. Set all bugs that were "Fix Committed" to "Fix Released"

.. _PEP 8: http://www.python.org/dev/peps/pep-0008/
.. _unittest: http://docs.python.org/library/unittest.html
.. _~testtools-dev: https://launchpad.net/~testtools-dev
.. _MIT license: http://www.opensource.org/licenses/mit-license.php
.. _Sphinx: http://sphinx.pocoo.org/
.. _restructuredtext: http://docutils.sourceforge.net/rst.html
