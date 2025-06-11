---
tags:
  - exercise
source: "[[Algebra Notes From the Underground]]"
---
Let $R$ be a ring. Prove that $(2(1_R)) \cdot (3(1_R)) = 6(1_R)$. More generally, give an argument showing that $(m1_R)\cdot(n1_R) = (mn)1_R$. (Show that for all $a \in R, (m1_R) \cdot a = ma$. You may assume that $m$ is nonnegative. Why?) 

>[!answer]-
> By direct computation, we have
> $$
> 2(1_R) \cdot (3(1_R)) = (1_R + 1_R) \cdot (1_R + 1_R + 1_R) = (1_R + 1_R + 1_R + 1_R + 1_R + 1_R) = 6(1_R)
> $$
> Now we will prove this in general. Let $a \in R$ and $m \in \mathbb{Z}$. We will prove that $m1_R \cdot a = ma$. We may assume that nonnegative. We will now proceed by induction.
> 
> Base case ($m = 0$):
> By definition, $0(1_R) \cdot a  = 0_R \cdot a = 0a$.
> Inductive step:
> Suppose that $m1_R \cdot a = ma$ for some $m \ge 0$. Then, 
> $$
> (m +1)1_R \cdot a = (m1_R + 1_R) \cdot a = m1_R \cdot a + 1_R \cdot a = ma + a = (m+1)a
> $$
> Thus, $m1_R \cdot a = ma$ for all $a \in R, m \in \mathbb{Z}$. Then, $(m1_R) \cdot (n1_R) = m(n1_R)$ which is $m$ groups of $n$ times of $1_R$, that is $mn$ times of $1_R$. Thus, $(m1_R) \cdot (n1_R) = (mn)1_R$. $\blacksquare$
> 


