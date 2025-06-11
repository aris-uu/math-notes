---
tags:
  - exercise
source: "[[Algebra Notes From the Underground]]"
---
Prove that if $R$ is an integral domain, then $R[x]$ is also an integral domain.

>[!answer]-
> Let $R$ be an integral domain. Now, consider $R[x]$. Clearly, $0 \neq 1$. Now, let $a, b \in R[x]$ such that $ab = 0$. Suppose both $a$ and $b$ are nonzero, then $a = a_0 + a_1x + \cdots + a_nx^n$ and $b = b_0 + b_1x + \cdots + b_mx^m$ where $\deg(a) = n$ and $\deg(b) = m$. Then, the coefficient of $x^{m+n}$ in $ab$ is $a_nb_m$. However, $ab = 0$. Therefore $a_nb_m = 0$. Since $R$ is an integral domain, it must be that $a_n = 0$ or $b_m = 0$, but the leading coefficient of a polynomial can't be zero. Therefore, our assumption is false and thus, $a = 0$ or $b = 0$. Therefore, $R[x]$ is also an integral domain. $\blacksquare$

