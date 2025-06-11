---
tags:
  - exercise
source: "[[Algebra Notes From the Underground]]"
---
The 'characteristic' of a ring $R$ is the smallest positive integer $n$ such that $n(1_R) = 0_R$, or $0$ if there is no such positive integer.
- Show that the characteristic of $\mathbb{Z}$ is 0, and the characteristic of $\mathbb{Z}/m\mathbb{Z}$ is $m$.
- Show that if $R$ has characteristic $n$, then $na = 0_R$ for all elements $a$ of $R$.

>[!answer]-
> In $\mathbb{Z}$, if $n > 0$, then $n\cdot 1 = n > 0$. Thus, there is no such positive integer such that $n \cdot 1 = 0$. Therefore, the characteristic is $0$. In $\mathbb{Z}/m\mathbb{Z}$, $m[1] = [m] = [0]$. Suppose there is another positive integer $n < m$ for which $n[1]= [0]$. Then, $[n] = [0]$, so $m$ must divide $n$, but $0 < n < m$ so this is not possible. Thus, the characteristic is $m$. 
> 
> Let $R$ be a ring with characteristic $n$. Then, by [[Exercise 3.8]], we have $na = (n1_R) \cdot a$. Since $n$ is the characteristic of $R$. $n(1_R) = 0_R$. Thus, $na = 0_Ra = 0_R$. $\blacksquare$

