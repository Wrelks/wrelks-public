---
layout: article
title: Simon's Algorithm
cover: /images/simon's-algorithm-qiskit.png
key: svga3473gfmr
comment: false
aside:
  toc: true
author: Aditya
---

<br>

<!--more-->

## Background

In the year 1994, Daniel Simon formulated a computational problem, called Simon's Problem, that could be solved exponentially faster by a quantum algorithm running on a quantum computer than by any deterministic or probabilistic classical algorithm running on a classical computer. Despite it being a problem with little to no practical value, it is well known as the first quantum algorithm to demonstrate this exponential speedup over its classical counterparts and is said to have been the "inspiration" for the much more famous Shor's Algorithm.

## Problem

The problem is presented in the form of a function $f$ that maps $n$-bit input strings to $n$-bit output strings ...
$$f: \{0,1\}^n \rightarrow \{0,1\}^n$$
... satisfying the property that for any two $n$-bit strings $x$ and $y$, $f(x) = f(y)$ only if $x \oplus s = y$, where $s$ is an unknown $n$-bit string.\

Or more formally:
$$
f: \{0,1\}^n \rightarrow \{0,1\}^n\:\:\vert\:\: f(x) = f(x \oplus s) \:\:\forall x \in \{0,1\}^n 
$$

Note that $\oplus$ represents bitwise addition modulo 2, or a simple bitwise XOR.

If $s$ were the string consisting of $n$ zeros, $f$ would become a one-to-one function, since no two inputs would give the same output. In the more likely case that $s$ is some other arbitrary string, $f$ becomes a two-to-one function.

> An example:  
  If $n = 2$, and $s = 11$  
  $f(00) = f(00 \oplus s) = f(11)$
  $f(01) = f(01 \oplus s) = f(10)$

So what's the problem? **We don't know the value of $s$.** 

Given a black box of some kind that implements $f$ (called an _oracle_), we need to devise a way to figure out what $s$ is.

## Complexity 

A naive classical solution to this problem would be to take the oracle and feed it different $n$-bit input strings, recording the output each time. When we find 2 inputs $x$ and $y$ that give us the same output, we stop the process. We know that a bitwise XOR of either input with the secret string $s$ must give us the other. By the properties of the XOR operator, this also means that $s = x \oplus y$, and so $s$ is easily computed.

But here's the catch: an $n$-bit binary string can take on $2^n$ different values. If you were to try each one of these, how long would it take before you found a collision?
- In the worst case, if $f$ was one-to-one, or if you just got very unlucky with the inputs you picked, you would need to test 1 more than half of all possible inputs to either deduce that $f$ was one-to-one or to find a collision respectively.
- In the best case, our first 2 inputs would collide and we'd be done.
- In the general case, we would have to guess about $\Omega(\sqrt{2^n})$ different times before being _likely_ to find a collision. This is similar to the [birthday problem](https://en.wikipedia.org/wiki/Birthday_problem).

However, even $\sqrt{2^n} = 2^{n/2}$ is still an exponential growth in $n$, and such algorithms are not good for our computers, especially on large inputs. We need a better algorithm...

## Simon's Algorithm