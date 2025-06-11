---
tags:
  - exercise
source: "[[Algebra Notes From the Underground]]"
title: Exercise 3.1
---
Consider the set $5 \mathbb{Z}$ of integer multiples of 5. We have seen that this is not a ring with the usual operations (cf. Example 3.5; it is at best a rng). However, consider the usual addition and the following different multiplication:

$$
a \odot b := \frac{ab}{5}
$$
Verify that $5\mathbb{Z}$ is closed with respect to this operation, and that $(5\mathbb{Z}, +, \odot)$ is a ring according to Definition 3.1.

>[!answer]-
> We will first verify that $a \odot b$ is closed in $5 \mathbb{Z}$. Let $a, b \in 5\mathbb{Z}$. Then, $a = 5k$ and $b = 5n$ for some $n, k \in \mathbb{Z}$. Therefore, 
> $$
> a \odot b = \frac{ab}{5} = \frac{25nk}{5} = 5nk \in 5\mathbb{Z} .
> $$ 
> Thus, it is closed. 
> 
> Now, we will verify that it is associative. Let $a, b, c \in 5\mathbb{Z}$. Then,
> $$
> (a \odot b) \odot c = \frac{\frac{ab}{5}c}{5} = \frac{abc}{25} = \frac{a\frac{bc}{5}}{5} = a \odot (b \odot c)
> $$
> Thus, it is associative. 
> Lastly, we will verify that distributivity holds. Let $a, b, c \in 5\mathbb{Z}$. Then,
> $$
> a \odot (b + c) = \frac{a(b + c)}{5} = \frac{ab + ac}{5} = \frac{ab}{5} + \frac{ac}{5} = (a\odot b) + (a \odot c)
> $$
> The proof for right distributivity is similar. Since the addition is derived, the property for addition holds automatically. Thus, $(5\mathbb{Z}, +, \odot)$ is a ring.
 
 



