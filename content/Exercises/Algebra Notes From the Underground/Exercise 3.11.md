---
tags:
  - exercise
source: "[[Algebra Notes From the Underground]]"
---
A 'Boolean ring' is a ring $R$ such that $\forall a \in R, a^2 = a$.
- Prove that for all $a$ in a Boolean ring, $2a = 0$.
- Prove that Boolean rings are *commutative*, that is, $a b = b a$ for all $a, b$. 
Hint: Consider $(a + a)^2, (a + b)^2$ 

>[!answer]-
> Let $R$ be a Boolean ring.
> 
> a. Let $a \in R$. Since $R$ is a Boolean ring, $2a = a + a = (a + a)^2 = a^2 + a^2 + a^2 + a^2 = 4a^2 = 4 a$. Thus, $2a = 0$.
> 
> b. Let $a, b \in R$.  Since $R$ is a Boolean ring, $a + b = (a + b)^2 = a^2 + b a + a b + b^2 = a + b a + a b + b$. Thus, $b a + a b = 0$. Thus, $b a = -a b$. From part a, we have $a = -a$ for all $a \in R$ . Therefore, $b a = - a b = a b$. $\blacksquare$    
