1.2.3 (2018-10-30)
==================

Bug Fixes
---------

- Fixed a bug which prevented installation of editable vcs requirements with subdirectory specifiers.  #91


1.2.2 (2018-10-29)
==================

Bug Fixes
---------

- Fixed a bug which prevented mercurial repositories from acquiring commit hashes successfully.  #89


1.2.1 (2018-10-26)
==================

Bug Fixes
---------

- Fixed an issue which caused accidental leakage of open ``requests.session`` instances.  #87


1.2.0 (2018-10-24)
==================

Features
--------

- ``Pipfile`` and ``Lockfile`` models will now properly perform import and export operations with fully data serialization.  #83
  
- Added a new interface for merging ``dev`` and ``default`` sections in both ``Pipfile`` and ``Lockfile`` objects using ``get_deps(dev=True, only=False)``.  #85
  

Bug Fixes
---------

- ``Requirement.as_line()`` now provides an argument to make the inclusion of markers optional by passing ``include_markers=False``.  #82
  
- ``Pipfile`` and ``Lockfile`` models are now able to successfully perform creation operations on projects which currently do not have existing files if supplied ``create=True``.  #84


1.1.9 (2018-10-10)
==================

Bug Fixes
---------

- Fixed a bug in named requirement normalization which caused querying the index to fail when looking up requirements with dots in their names.  #79


1.1.8 (2018-10-08)
==================

Bug Fixes
---------

- Fixed a bug which caused VCS URIs to build incorrectly when calling ``VCSRequirement.as_line()`` in some cases.  #73
  
- Fixed bug that editable package with ref by @ is not supported correctly  #74


1.1.7 (2018-10-06)
==================

Bug Fixes
---------

- Add space before environment markers ; to make editable packages can be installed by pip  #70


1.1.6 (2018-09-04)
==================

Features
--------

- ``Requirement.get_commit_hash`` and ``Requirement.update_repo`` will no longer clone local repositories to temporary directories or local src directories in order to determine commit hashes.  #60
  
- Added ``Requirement.lock_vcs_ref()`` api for locking the VCS commit hash to the current commit (and obtaining it and determining it if necessary).  #64
  
- ``Requirement.as_line()`` now offers the parameter ``as_list`` to return requirements more suited for passing directly to ``subprocess.run`` and ``subprocess.Popen`` calls.  #67
  

Bug Fixes
---------

- Fixed a bug error formatting of the path validator method of local requirements.  #57
  
- Fixed an issue which prevented successful loads of ``Pipfile`` objects missing entries in some sections.  #59
  
- Fixed an issue which caused ``Requirement.get_commit_hash()`` to fail for local requirements.  #67


1.1.5 (2018-08-26)
==================

Bug Fixes
---------

- Fixed an issue which caused local file uri based VCS requirements to fail when parsed from the ``Pipfile`` format.  #53


1.1.4 (2018-08-26)
==================

Features
--------

- Improved ``Pipfile.lock`` loading time by lazily loading requirements in favor of quicker access to metadata and text.  #51


1.1.3 (2018-08-25)
==================

Bug Fixes
---------

- Fixed a bug which caused wheel requirements to include specifiers in ``Requirement.as_line()`` output, preventing installation when passing this output to pip.  #49


1.1.2 (2018-08-25)
==================

Features
--------

- Allow locking of specific vcs references using a new api: ``Requirement.req.get_commit_hash()`` and ``Requirement.commit_hash`` and updates via ``Requirement.req.update_repo()``.  #47


1.1.1 (2018-08-20)
==================

Bug Fixes
---------

- Fixed a bug which sometimes caused extras to be dropped when parsing named requirements using constraint-style specifiers.  #44
  
- Fix parsing error in `Requirement.as_ireq()` if requirement contains hashes.  #45


1.1.0 (2018-08-19)
==================

Features
--------

- Added support for ``Requirement.get_dependencies()`` to return unpinned dependencies.
  Implemented full support for both parsing and writing lockfiles.
  Introduced lazy imports to enhance runtime performance.
  Switch to ``packaging.canonicalize_name()`` instead of custom canonicalization function.
  Added ``Requirement.copy()`` to the api to copy a requirement.  #33
  
- Add pep423 formatting to package names when generating ``as_line()`` output.
  Sort extras when building lines.
  Improve local editable requirement name resolution.  #36
  

Bug Fixes
---------

- - Fixed a bug which prevented dependency resolution using pip >= 18.0.

  - Fix pipfile parser bug which mishandled missing ``requires`` section.  #33
  
- Fixed a bug which caused extras to be excluded from VCS urls generated from pipfiles.  #41
  

Vendored Libraries
------------------

- Unvendored ``pipfile`` in favor of ``plette``.  #33
  

Removals and Deprecations
-------------------------

- Unvendored ``pipfile`` in favor of ``plette``.  #33
  
- Moved pipfile and lockfile models to ``plette`` and added api wrappers for compatibility.  #43


1.0.11 (2018-07-20)
===================

Bug Fixes
---------

- If a package is stored on a network share drive, we now resolve it in a way that gets the correct relative path (#29)
- Properly handle malformed urls and avoid referencing unbound variables. (#32)


1.0.10 (2018-07-11)
===================

Bug Fixes
---------

- Fixed a bug which prevented the inclusion of all markers when parsing requirements from existing pipfile entries.  `pypa/pipenv#2520 <https://github.com/pypa/pipenv/issues/2520>`_ (#26)
- requirementslib will now correctly handle subdirectory fragments on output and input for both pipfile and pip-style requirements. (#27)


1.0.9 (2018-06-30)
==================

Features
--------

- Move slow imports to improve import times. (#23)

Bug Fixes
---------

- Use ``hostname`` instead of ``netloc`` to format urls to avoid dropping usernames when they are included. (#22)


1.0.8 (2018-06-27)
==================

Bug Fixes
---------

- Requirementslib will no longer incorrectly write absolute paths or uris where relative paths were provided as inputs.
- Fixed a bug with formatting VCS requirements when translating implicit SSH URIs to ssh URLs. (#20)


1.0.7 (2018-06-27)
==================

Bug Fixes
---------

- Fixed an issue with resolving certain packages which imported and executed other libraries (such as ``versioneer``) during ``setup.py`` execution. (#18)


1.0.6 (2018-06-25)
==================

Bug Fixes
---------

- Fixed a quotation error when passing markers to ``Requirement.constraint_line`` and ``Requirement.markers_as_pip``. (#17)


1.0.5 (2018-06-24)
==================

Features
--------

- Cleaned up relative path conversions to ensure they are always handled in
  posix style. (#15)


1.0.4 (2018-06-24)
==================

Bug Fixes
---------

- Fixed a bug which caused converting relative paths to return ``None``. (#14)


1.0.3 (2018-06-23)
==================

Bug Fixes
---------

- Fixed a bug which caused the base relative path to be listed as ``./.``
  instead of ``.``. (#12)
- Fixed a bug that caused egg fragments to be added to
  ``Requirement.as_line()`` output for file requirements. (#13)


1.0.2 (2018-06-22)
==================

Bug Fixes
---------

- Fixed a problem with loading relative paths in pipfiles with windows-style
  slashes. (#11)
- Fixed a bug with default values used during lockfile generation. (#9)

Improved Documentation
----------------------

- Fixed usage documentation. (#9)


1.0.1 (2018-06-15)
==================

Features
--------

- Updated automation scripts to add release scripts and tagging scripts.
  (1-d0479c0a)

Bug Fixes
---------

- Fix parsing bug with local VCS uris (1-22283f73)
- Fix bug which kept vcs refs in local relative paths (2-34b712ee)

Removals and Deprecations
-------------------------

- Cleanup unused imports and migrate history file to changelog. (1-1cddf326)


1.0.0 (2018-06-14)
==================

Features
--------

- Add pipfile parser to parse all requirements from pipfile to requirement
  format and generate pipfile hashes.
- Add towncrier.
- Reorganize and reformat codebase, refactor.
- Implement lockfile parser and allow it to output to requirements.txt format.
- Better parsing of named requirements with extras.
- Add constraint_line property for pip constraintfile input.
- Rewrite parser logic for cleanliness and consistency.
- Add lockfile parser and allow it to output to requirements format.
- Reorganize and format codebase, refactor code.
- Normalize windows paths for local non-vcs requirements.

Bug Fixes
---------

- Normalize windows paths for local non-vcs requirements.
- Fixed a bug which mixed posix-style and windows-style path separators for
  relative paths.
- Raise an explicit error when handling the current directory as a requirement
  if it isn't installable.
- Bugfix for local file requirements which had their URIs inappropriately
  truncated.
- Requirement line output will now properly match the URI scheme supplied at
  creation time.
- Fixed a bug with path resolution related to ramdisks on windows.
- Fix a bug which caused parsing to fail by adding extra whitespace to
  requirements.

Vendored Libraries
------------------

- Vendored patched pipfile


0.1.1 (2018-06-05)
==================

Updates
-------
 - Fix editable URI naming on windows.
 - Fixed a bug causing failures on `-e .` paths with extras.


0.1.0 (2018-06-05)
==================

Updates
-------
 - Fall back to pip/setuptools as a parser for setup.py files and project names.


0.0.9 (2018-06-03)
==================

Updates
-------
 - Bugfix for parsing setup.py file paths.


0.0.8 (2018-06-xx)
==================

Updates
-------
 - Resolve names in setup.py files if available.
 - Fix a bug with populating Link objects when there is no URI.
 - Properly unquote URIs which have been urlencoded.


0.0.7 (2018-05-26)
==================

Updates
-------
 - Parse wheel names.


0.0.6 (2018-05-26)
==================

Updates
-------
 - Fix windows relative path generation.
 - Add InstallRequirement generation.


0.0.5 (2018-05-25)
==================

Updates
-------
 - Bugfix for parsing editable local paths (they were being parsed as named requirements.)


0.0.4 (2018-05-25)
==================

Updates
-------
 - Bugfix.


0.0.3 (2018-05-10)
==================

Updates
-------
 - Bugfix for including egg fragments in non-vcs urls.


0.0.2 (2018-05-10)
==================

Updates
-------
 - Fix import bug.


0.0.1 (2018-05-10)
==================

Updates
-------
 - Bugfixes for remote files and zipfiles, extras on urls.
 - Initial commit
