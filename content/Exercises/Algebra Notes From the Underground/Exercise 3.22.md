---
tags:
  - exercise
source: "[[Algebra Notes From the Underground]]"
---
Suppose the set $R$ consists of four elements: $R = \{0, 1, x, y\}$, and two operations $+$ and $\cdot$ are defined on $R$, with the following multiplication tables:

|  +  |  0  |  1  |  x  |  y  |
|:---:|:---:|:---:|:---:|:---:|
|  0  |  0  |  1  |  x  |  y  |
|  1  |  1  |  0  |  y  |  x  |
|  x  |  x  |  y  |  0  |  1  |
|  y  |  y  |  x  |  1  |  0  |

| $\cdot$ |  0  |  1  |  x  |  y  |
| :-----: | :-: | :-: | :-: | :-: |
|    0    |  0  |  0  |  0  |  0  |
|    1    |  0  |  1  |  x  |  y  |
|    x    |  0  |  x  |  y  |  1  |
|    y    |  0  |  y  |  1  |  x  |
Prove that $R$ is a field. (It would take too long to verify completely the associativity of $+$ and $\cdot$ and the distributivity axiom. They happen to work in this case; please illustrate this fact by choosing an example for each of these properties. On the other hand, make sure you give a complete verification for the other axioms needed to prove that $R$ is a field.)

>[!answer]-
> The addition and multiplication are clearly closed based on the table.
> 1. Commutativity of addition. Since the table is symmetric, it is commutative.
> 2. Additive identity. 0 is the additive identity, can be seen from the first row and column.
> 3. Associativity of addition. (0 + 1) + x = 1 + x = y = 0 + y = 0 + (1 + x)
> 4. Additive inverse. Each element has an additive inverse since each row has a 0.
> 5. Commutativity of multiplication. Since the table is symmetric, it is commutative.
> 6. Associativity of multiplication. 1(xy) = 1(1) = 1 = xy = (1x)y
> 7. Multiplicative identity. 1 is the multiplicative identity, can be seen from the second row and column.
> 8. Distributivity. x(y + y) = x0 = 0 = 1 + 1 = xy + xy
> 9. Multiplicative inverse. Each nonzero element has a multiplicative inverse since each nonzero row has a 1.
 
