---
tags:
  - exercise
source: "[[Algebra Notes From the Underground]]"
---
Prove that the characteristic of an integral domain is a prime integer.

>[!answer]-
> Let $R$ be an integral domain with characteristic $n$. First we will prove that $n \neq 1$. Suppose $n = 1$, then it follows that $1 = 0$, but this is a contradiction since an integral domain is nontrivial. Thus, $n \neq 1$. If $n = 0$, then $n$ is prime. So, consider the case $n > 1$. Suppose $n \vert ab$. Then, $ab = nk$ for some integer $k$. In the ring $R$, this equation becomes, $(ab)1_R = n(k1_R) = 0$ since the characteristic is $n$. Now, we have $(a1_R)(b1_R) = 0$. Since $R$ is an integral domain, we have either $a1_R = 0$ or $b1_R = 0$. Thus, by the [[characteristic divisibility lemma]], we have $n \vert a$ or $n \vert b$. So, $n$ is prime. $\blacksquare$

