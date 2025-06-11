---
tags:
  - exercise
source: "[[Algebra Notes From the Underground]]"
---
Define a new 'multiplication' operation on $\mathbb{Z}$, by setting $a \odot b = -ab$. Is $(\mathbb{Z}, +, \odot)$ a ring according to Definition 3.1? (Prove it is, or explain why it is not).

>[!answer]-
> Yes, it is a ring. The properties of addition follows from $\mathbb{Z}$. First, we will prove that the multiplication is associative. Let $a,b,c \in \mathbb{Z}$. Then,
> $$
> a \odot (b \odot c) = -a(-bc) = abc = -((-ab)c) = (a \odot b) \odot c
> $$
> Next, we will prove that distributivity holds.
> $$
> \begin{align*}
> a \odot (b + c) &= -a (b+c) = -(ab + ac) = -ab + (-ac) = a\odot b + a\odot c \\
> (a + b) \odot c &= -(a + b)c = -(ac + bc) = -ac + (-bc) = a\odot c + b\odot c 
> \end{align*}
> $$
> Lastly, we will prove that the multiplicative identity exists. Choose $-1$ as the identity. Let $a \in \mathbb{Z}$. Then,
> $$
> \begin{align*}
> -1 \odot a = - (-1(a)) = a \\
> a \odot -1 = -a(-1) = a
> \end{align*}
> $$
> Thus, $(\mathbb{Z}, +, \odot)$ is a ring. $\blacksquare$
> 

