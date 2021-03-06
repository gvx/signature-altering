signature-altering
==================

This package helps you create decorators that alter the signatures of
decorated functions in predictable ways, namely inserting/removing
arguments from the front and inserting/removing keyword arguments.

-----

.. contents:: **Table of Contents**
    :backlinks: none

Usage
-----

The simplest way to use signature-altering looks like this::

    @decorator
    def no_op_decorator(f, *args, **kwargs):
        return f(*args, **kwargs)

For the rest of the examples we will assume the decorator will be used
as follows::

    @spam
    def ham(a, b):
        return a + b

Suppose we want ``ham`` to behave like this::

    >>> ham(100, 2, 3)
    95

We would need to provide a definition of ``spam`` like this::

    @decorator
    def spam(f, prefix, *args, **kwargs):
        return prefix - f(*args, **kwargs)

Note that ``ham`` now has a different signature from how it was defined.

If we, on the other hand, want to supply fewer arguments, like this::

    >>> ham(7)
    107

We would do this::

    @decorator(insert_args=1)
    def spam(f, *args, **kwargs):
        return f(100, *args, **kwargs)

Keyword arguments work mostly the same, except we need to supply the names
when inserting them::

    @decorator(insert_kwargs='a b')
    def spam(f, *args, **kwargs):
        return f(*args, a=7, b=5, **kwargs)

Installation
------------

signature-altering is distributed on `PyPI <https://pypi.org>`_ as a universal
wheel and is available on Linux/macOS and Windows and supports
Python 3.5+ and PyPy.

::

    $ pip install signature-altering

License
-------

signature-altering is distributed under the terms of the
`MIT License <https://choosealicense.com/licenses/mit>`_.
