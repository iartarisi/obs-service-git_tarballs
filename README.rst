=========================================
 OBS service for downloading git tarballs
=========================================

This is an `Open Build Service`_ source service. It downloads a tarball and parses its git ChangeLog file for information about recent changes which then go to the package's .changes file.

The ``Version`` field will be set to
``%(tarball_version)s+git.%(timestamp)s.%(commit_sha)s``. Where
``tarball_version`` is the version as read from the parent directory
inside the downloaded tarball - everything after the last dash (``-``)
in the directory's name. ``timestamp`` is the current seconds from the
UNIX epoch when the source service was run (if there were new
changes). ``commit_sha`` is the latest commit sha hash from the
ChangeLog file.

The ``git_tarballs`` service will also change the specfile's ``Source:``
to the ``filename`` argument of the service and the ``%setup -q`` line
to match the parent folder name in the tarball.

On the first run, ``git_tarballs`` will just set the spec file's
``Version`` field to the latest git commit. The .changes file will only
be updated with commit message information when newer commits (compared
to the one now set in ``Version``) are found.

Up to date requirements are kept in the files ``pip-requires`` and
``test-requires``

To run the testsuite, just use ``nosetests`` or ``python -m unittest
discover`` (on python2.7).

TODO

* use current user's email address in .changes file
* stop parsing when we reach the last known commit
* tests


.. _Open Build Service: http://openbuildservice.org/
.. _python-mock: http://www.voidspace.org.uk/python/mock/mock.html
