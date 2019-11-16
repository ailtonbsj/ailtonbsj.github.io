---
layout: post
title:  "Simplifying Boolean Logic Expressions with SymPy"
date:   2019-10-20 14:44:00 -0300
categories: tutorial linux hardware
---
The last tutorial about Boolean Algebra we use PyEDA to generate a lot of Truth Table and expressions. Now we will go to use the module of Python 3 called SymPy. This module is so powerfull to simplify boolean expressions.

First import the module:
```python
from sympy import *
```

Then create the symbolic variables:
```python
a, b, c = symbols('a, b, c')
```

Now we can create our expressions:
```python
s0 = a & b & c | a & ~c | a & ~b
s1 = (~a & ~b & ~c) | (~a & b & ~c) | (a & ~b & c)
s2 = ~a & ~b & ~c | ~a & b & c | ~a & b & ~c | a & ~b & ~c | a & b & ~c
s3 = (a | b | c) & (~a | ~b | c)
```

And to simplify the expression with `simplify_logic`:
```python
simplify_logic(s0)
# Output: a
simplify_logic(s1)
# Ouput: (a | ~c) & (c | ~a) & (~a | ~b)
simplify_logic(s2)
# Output: ~c | (b & ~a)
simplify_logic(s3)
# Output: c | (a & ~b) | (b & ~a)
```

Or to simplify with `to_dnf`:
```python
to_dnf(s0, True)
# Output: a
to_dnf(s1, True)
# Ouput: (~a & ~c) | (a & c & ~b)
to_dnf(s2, True)
# Output: ~c | (b & ~a)
to_dnf(s3, True)
# Output: c | (a & ~b) | (b & ~a)
```

Or to simplify with `to_cnf`:
```python
to_cnf(s0, True)
# Output: a
to_cnf(s1, True)
# Ouput: (a | ~c) & (c | ~a) & (~a | ~b)
to_cnf(s2, True)
# Output: (b | ~c) & (~a | ~c)
to_cnf(s3, True)
# Output: (a | b | c) & (c | ~a | ~b)
```