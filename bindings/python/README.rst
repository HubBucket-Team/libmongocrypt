============
PyMongoCrypt
============
:Info: Python bindings for libmongocrypt. See `GitHub <github.com/mongodb/libmongocrypt>`_ for the latest source.
:Author: Shane Harvey

About
=====

Python wrapper library for libmongocrypt that supports client side encryption
in drivers. PyMongoCrypt uses `cffi <https://pypi.org/project/cffi/>`_.

**Support for client side encryption is in beta. Backwards-breaking changes
may be made before the final release.**

PyMongoCrypt supports Python 2.7, 3.4+, and PyPy3.5+.

Support / Feedback
==================

For issues with, questions about, or feedback for PyMongoCrypt, please look into
our `support channels <http://www.mongodb.org/about/support>`_. Please
do not email any of the PyMongoCrypt developers directly with issues or
questions - you're more likely to get an answer on the `mongodb-user
<http://groups.google.com/group/mongodb-user>`_ list on Google Groups.

Bugs / Feature Requests
=======================

Think you’ve found a bug? Want to see a new feature in PyMongoCrypt?
Please open a case in our issue management tool, JIRA:

- `Create an account and login <https://jira.mongodb.org>`_.
- Navigate to `the PYTHON project <https://jira.mongodb.org/browse/PYTHON>`_.
- Click **Create Issue** - Please provide as much information as possible about the issue type and how to reproduce it.

Bug reports in JIRA for all driver projects (i.e. PYTHON, CSHARP, JAVA) and the
Core Server (i.e. SERVER) project are **public**.

How To Ask For Help
-------------------

Please include all of the following information when opening an issue:

- Detailed steps to reproduce the problem, including full traceback, if possible.
- The exact python version used, with patch level::

  $ python -c "import sys; print(sys.version)"

- The exact version of PyMongoCrypt used::

  $ python -c "import pymongocrypt; print(pymongocrypt.__version__)"

- The exact version of libbmongocrypt used by PyMongoCrypt::

  $ python -c "import pymongocrypt; print(pymongocrypt.libmongocrypt_version())"

- The exact version of PyMongo used (if applicable), with patch level::

  $ python -c "import pymongo; print(pymongo.version); print(pymongo.has_c())"

- The operating system and version (e.g. Windows 7, OSX 10.8, ...)
- Web framework or asynchronous network library used, if any, with version (e.g.
  Django 1.7, mod_wsgi 4.3.0, gevent 1.0.1, Tornado 4.0.2, ...)

Security Vulnerabilities
------------------------

If you've identified a security vulnerability in a driver or any other
MongoDB project, please report it according to the `instructions here
<http://docs.mongodb.org/manual/tutorial/create-a-vulnerability-report>`_.

Installation
============

PyMongoCrypt can be installed with `pip <http://pypi.python.org/pypi/pip>`_::

  $ python -m pip install pymongocrypt

You can also download the project source and do::

  $ python -m pip install .


Installing libmongocrypt
------------------------

PyMongoCrypt ships wheels for macOS and Windows that include an embedded
libmongocrypt build. For Linux users libmongocrypt needs to be installed
manually.

libmongocrypt is [continuously built and published on evergreen]
(https://evergreen.mongodb.com/waterfall/libmongocrypt).
The latest tarball containing libmongocrypt built on all supported variants is
(published here)[https://s3.amazonaws.com/mciuploads/libmongocrypt/all/master/latest/libmongocrypt-all.tar.gz].

Download and extract ``libmongocrypt-all.tar.gz`` and set
``PYMONGOCRYPT_LIB`` to the path to your operating system's libmongocrypt.so file.
For example::

  $ export PYMONGOCRYPT_LIB='/path/to/libmongocrypt.so'
  $ python -c "import pymongocrypt; print(pymongocrypt.libmongocrypt_version())"

Dependencies
============

PyMongoCrypt supports CPython 2.7, 3.4+, PyPy, and PyPy3.5+.

PyMongoCrypt requires `cffi <https://pypi.org/project/cffi/>`_.

PyMongoCrypt also requires libmongocrypt to be installed on your
system. If libmongocrypt is not installed you will see an error
like this:

.. code-block:: python

  >>> import pymongocrypt
  Traceback (most recent call last):
    File "<stdin>", line 1, in <module>
    File "pymongocrypt/__init__.py", line 15, in <module>
      from pymongocrypt.binding import libmongocrypt_version, lib
    File "pymongocrypt/binding.py", line 803, in <module>
      lib = ffi.dlopen(os.environ.get('PYMONGOCRYPT_LIB', 'mongocrypt'))
    File "/.../lib/python3.7/site-packages/cffi/api.py", line 146, in dlopen
      lib, function_cache = _make_ffi_library(self, name, flags)
    File "/.../lib/python3.7/site-packages/cffi/api.py", line 828, in _make_ffi_library
      backendlib = _load_backend_lib(backend, libname, flags)
    File "/.../lib/python3.7/site-packages/cffi/api.py", line 823, in _load_backend_lib
      raise OSError(msg)
  OSError: ctypes.util.find_library() did not manage to locate a library called 'mongocrypt'


Use the ``PYMONGOCRYPT_LIB`` environment variable to load a locally installed
libmongocrypt build without relying on platform specific library path environment
variables, like ``LD_LIBRARY_PATH``. For example::

  $ export PYMONGOCRYPT_LIB='/path/to/libmongocrypt.so'
  $ python -c "import pymongocrypt; print(pymongocrypt.libmongocrypt_version())"


Documentation
=============

You will need `sphinx <https://pypi.org/project/Sphinx/>`_ installed to generate the
documentation. Documentation can be generated by running **python
setup.py doc**. Generated documentation can be found in the
*doc/build/html/* directory.

Testing
=======

The easiest way to run the tests is to run **python setup.py test** in
the root of the distribution.
