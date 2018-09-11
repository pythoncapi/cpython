Design a new better C API for Python
====================================

This project is a fork of the development version of the future CPython 3.8.
The intent is to experiment to implement the new C API described at:

   https://pythoncapi.readthedocs.io/

Install dependencies on Fedora::

   dnf install -y make gcc check

Build and run unit tests::

   ./configure --enable-shared --with-pydebug
   make
   cd capi_tests
   make  # only test Py_NEWCAPI
   # or to run the full test matrix: make testmatrix

If you want to help, look at ``TODO.rst``.

The changes live in the **pythoncapi** branch.

New C API defines:

* ``Py_NEWCAPI_NO_MACRO``: replace macros with function calls
  ``PyTuple_GET_SIZE()`` becomes ``PyTuple_Size()``
* ``Py_NEWCAPI_NO_STRUCT``: must not use ``PyObject.ob_refcnt`` or any other
  field of Python object structures; structures should hide their fields:
  compilation error.
* ``Py_NEWCAPI``: new C API without borrowed references, without macro,
  without struct

Related defines:

* ``Py_NEWCAPI_BORROWED_REF``: declare functions/macros using
  borrowed references -- enabled by ``Py_NEWCAPI_NO_MACRO``
  and ``Py_NEWCAPI_NO_STRUCT``, but not by ``Py_NEWCAPI``.

See also:

* `github.com/pythoncapi/cpython <https://github.com/pythoncapi/cpython>`_
* `capi-sig mailing list
  <https://mail.python.org/mm3/mailman3/lists/capi-sig.python.org/>`_
