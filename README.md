# `julialg`
_Julia-style arrays in Python_

Python library for mimicking Julia LinearAlgebra array indexing style and display formatting.

Test Result: [![CircleCI](https://circleci.com/gh/JWKennington/julialg/tree/master.svg?style=svg)](https://circleci.com/gh/JWKennington/julialg/tree/master)


## Motivation and Summary
Julia's `LinearAlgebra` package has some nice features, some of which are easier to emulate in Python than others. When 
comparing the results of Python code vs Julia code, it is annoying to have to mentally switch between the 0-indexed nature of 
Python and the 1-indexed nature of Julia. Also, the Julia arrays have a prettier array.
 
This package wraps numpy n-dimensional arrays in a new class, `JulArray`, and allows for 1-indexed slicing (more mathematically intuitive) 
instead of 0-indexed slicing (computer science convention). Also improves the prettiness of the representation of the 
array in a manner similar to Julia's LinearAlgebra package. To be clear, this is a Python package, meant to bring some 
of the elegance of Julia's interface for tensors to the Python setting


## Indexing
The `JulArray` class wraps a `numpy.ndarray` but overrides the getitem syntax to allow for 1-indexed style instead of
the default 0-indexed style. For example:
```python
>>> import numpy, julialg

# Create a numpy array
>>> a = numpy.arange(1, 11).reshape((2, 5))

# Create a JulArray from the numpy array
>>> j = julialg.JulArray(a)

# Index the numpy array using 0-indexed syntax
>>> a[0, 0:2]
array([1, 2])

# Index the JulArray using 1-indexed syntax
>>> j[1, 1:3].array
array([1, 2])
```

Notice in the above sample that the `JulArray` is able to convert both ints and slices from 1-indexed notation to
0-indexed notation to produce the same underlying numpy array. 

## Display
The `JulArray` overrides the default representation of the numpy array to be more cleanly formatted (like Julia arrays).
```python
>>> julialg.JulArray(numpy.arange(1.0, 11.0).reshape((2, 5)))
2x5 Array{float64,2}
  1.0000     6.0000
  2.0000     7.0000
  3.0000     8.0000
  4.0000     9.0000
  5.0000    10.0000
```
