---
layout: post
title:  "Working with PyEDA for solve questions of Digital Electronics"
date:   2019-10-20 14:44:00 -0300
categories: tutorial linux hardware
---
In this tutorial I will demonstrate some commands for using with Python to work with digital electronics. This tools is called PyEDA (Python Electronic Design Automation) and has some good features to use symbolic boolean algebra.

First of all let's to install the library. I'm using Ubuntu system, so:
```bash
sudo apt install python3
sudo apt install python3-dev
sudo apt install python2-pip
pip3 install pyeda
```

Now you need import the library. If you are using Python REPL, try:
```python
from pyeda.inter import *
```

To create the boolean variables use the command `exprvar`:
```python
a = exprvar('a')
b = exprvar('b')
c,d = map(exprvar, "cd")
```

You can create boolean expressions using the operators: `~`(NOT), `&` (AND), `|` (OR), `^` (XOR), `>>` (IMPLIES). For example:
```python
s0 = a | b
s1 = (a & c) | (a & b)
s2 = ~(a | b & c)
s5 = expr("a | ~b & c")
```

Using the method `equivalent` we can test if the expressions are equals:
```python
s0.equivalent(s1)
# Output: False
(~(a | b)).equivalent(~a & ~b)
# Output: True
```

You can create a Truth Table using the method `truthtable`:
```python
j,k = map(exprvar, "jk")
t3 = truthtable([k,j], "1001")
# Output
# j k
# 0 0 : 1
# 0 1 : 0
# 1 0 : 0
# 1 1 : 1

X = exprvars('x', 3)
t4 = truthtable(X, "101011-1")
# Output:
# x[2] x[1] x[0]
#    0    0    0 : 1
#    0    0    1 : 0
#    0    1    0 : 1
#    0    1    1 : 0
#    1    0    0 : 1
#    1    0    1 : 1
#    1    1    0 : -
#    1    1    1 : 1
```

Now we can convert expressions to Truth Table and inverse:
```python
s3 = truthtable2expr(t3)
# Output: Or(And(~j, ~k), And(j, k))
s4 = truthtable2expr(t4)
# Output: Or(And(~x[0], ~x[1], ~x[2]), And(~x[0], x[1], ~x[2]), And(~x[0], ~x[1], x[2]), And(x[0], ~x[1], x[2]), And(x[0], x[1], x[2]))

t0 = expr2truthtable(s0)
# Output:
# b a
# 0 0 : 0
# 0 1 : 1
# 1 0 : 1
# 1 1 : 1
t1 = expr2truthtable(s1)
# Output:
# c b a
# 0 0 0 : 0
# 0 0 1 : 0
# 0 1 0 : 0
# 0 1 1 : 1
# 1 0 0 : 0
# 1 0 1 : 1
# 1 1 0 : 0
# 1 1 1 : 1
```

Some utils method to expressions:
```python
s4 = ~(~a & a) & ~(b | ~c)
s4.simplify()
# Output: Not(Or(b, ~c))
s4.to_nnf()
# Output: And(~b, c)
```

## For more examples and documentation

- [PyEDA on GitHub](https://github.com/cjdrake/pyeda)
- [Python EDA Documentation](https://pyeda.readthedocs.io)