---
title: "Linear Recurrences 201"
date: 2025-04-25
permalink: /posts/2025/04/25/Linear-Recurrences-201
tags:
  - Generating Functions 
  - Linear Recurrences
  - Fibonnaci Numbers
comments: true
layout: single
---

While working through the details of the last post I discovered a beautiful result. It is by 
no means novel but it renders clear the relationship (which I neglected previously) between linear 
recurrences, ODEs and indeed anything which is 'sequence like'.

# Prerequisites
In this post we will take for granted knowledge of linear and abstract algebra. The exposition in 
general will be less motivated because there is a reasonably short path to the central theorem. 
We will adopt the same notation as in Linear Recurrences 101.

# Solution Spaces
In Linear Recurrences 101 we specified a particular sequence. That is, we prescribed a recurrence 
relation as well as some of the first terms, enough to uniquely pin down a sequence. If one does 
not provide any initial conditions then there are in fact many solutions to any given Linear Recurrence, 
and, these form an $$F$$ vector space. Indeed this vector space is a subspace of the vector space 
of sequences over $$F$$.


Let $$V = F^\mathbb{N}$$ be the set of all sequences in $$F$$. Then $$V$$ is an $$F$$ vector 
space. Moreover, the subset $$\{(a_n) \in V | a_n = \sum_{t=1}^k c_t a_{n-t} \text { } \forall n \geq k\}$$ is 
a subspace of $$V$$. In this framing, our work in Linear Recurrences 101 amounts to 
finding a basis for this subspace. One charactersiation of our approach is as follows. 

- We introduced an isomorphism between recurrence relations and polynomials (given by the characteristic polynomial) 
- We exploited the algebraic structure of the ring of polynomials to produce a simple factorisation. 
- We applied the inverse of the isomorphism to represent the solution of our original recurrence as a sum of solutions to simpler recurrences

A good deal of this was obscured by the use of The Chinese Remainder Theorem, but in essence the partial 
fraction decomposition reflects this factorisation, and the geometric series (and powers thereof) encode 
solutions to trivial recurrences of the form $$a_n = \lambda a_{n-1}$$ (we do not yet have the language to 
articulate 'powers' of recurrences). In the algebraic closure of a field this worked out rather nicely, but 
we required access to elements in the algebraic closure (not to mention knowledge of the solutions of the 
characteristic polynomial). We will see that even without the ability to reduce a polynomial to its linear 
factors similar analysis is possible.

# The Shift  Operator
Since we are now dealing with a vector space, it is helpful to couch our subspace in terms of a linear operator. 

**Definition (1): The Shift Operator**.
We call $$T: V \to V$$ defined by $$Ta_n = a_{n+1}$$ the shift operator. That is, 
$$Ta_n$$ is the sequence $$b_n$$, where $$b_n = a_{n+1}$$. $$T$$ is a linear operator on $$V$$.

The solution spaces of linear recurrences can be interpreted as kernels of polynomial functions of the 
Shift Operator, which are in turn linear operators. For example, the subspace of solutions to the reccurence 
$$a_n = \lambda a_{n-1}$$ is the kernel of the operator $$T - \lambda I$$. Notably, the solutions are precisely 
the $$\lambda$$ eigenspace of $$T$$! 

## Polynomials in the Shift Operator
Define $$T^n$$ to be the composition of the shift operator with itself $$n$$ times ($$T^0$$ is understood to be 
the identity). Then $$T^n$$ is also easily verified to be a linear operator and therefore 
$$p(T) = T^n - \sum_{t=1}^k c_tT^{n-t}$$ is a linear operator, and its kernel is the subspace of interest. 
Our question then is how does the subspace decompose? From our previous work we know that this decomposition 
is related the factorisation of $$p(z) \in F[z]$$. In fact, much of our previous work is still more or less applicable.

**Theorem (2)**.
Let $$V$$ be an $$F$$ vector space, $$p(z) \in F[z]$$ and $$p_1(z)p_2(z)\cdots p_s(z)$$ a pairwise coprime factorisation of $$p$$. 
For any operator $$T$$ on $$V$$, 

$$
\begin{equation*}
    \ker(p(T)) = \bigoplus_{i=1}^s \ker(p_i(T))
\end{equation*}
$$

**Proof of Theorem (2)**
First we need to set the stage. For a given $$T$$ we regard $$F[T]$$ as the ring of endomorphisms of the form $$\{\sum_{i=0}^n a_n T^n\}$$ 
under composition. The crux of our argument now (as it was previously) is that $$F[T]$$ is naturally isomorphic to $$F[z]$$ under multiplication. 
Arguing by induction, suppose $$p, q$$ are coprime. Then there are endomorphisms $$x(T), y(T)$$ such that 

$$
\begin{align*}
    x(T)p(T) + y(T)q(T) = I
\end{align*}
$$

then

$$
\begin{align*}
    (x(T)p(T))(v) + (y(T)q(T))(v) = v
\end{align*}
$$

for all $$v \in V$$. If $$v \in \ker(p(T)), \ker(q(T))$$, then the above shows that $$v$$ is in fact $$0$$. Moreover, 
if $$v \in \ker(pq(T))$$, then $$(x(T)p(T))(v) \in \ker(q(T))$$, and $$(y(T)q(T))(v) \in \ker(p(T))$$. Therefore, 

$$
\begin{equation*}
    \ker(pq(T)) = \ker(p(T)) \oplus \ker(q(T))
\end{equation*}
$$

as desired $$\square$$.

# Applications
The remarkable consequence of this theorem is that the solution space of a linear recurrence is a direct sum of the solution spaces 
of the sequences which correspond to its coprime factor polynomials. By way of example, the Fibonacci Numbers have characteristic 
polynomial $$x^2 - x - 1 = (x - \varphi)(x - (-\varphi^{-1}))$$. These factor polynomials correspond to the recurrences 
$$a_n = \varphi a_{n-1}$$ and $$b_n = -\varphi^{-1}b_{n-1}$$. These have solutions $$a_n = a_0 \varphi^n$$ and $$b_n = b_0 (-\varphi^{-1})^n$$ 
respectively. As we saw previously, the solution of the Fibonnaci recurrence was indeed of the form $$F_n = a_0 \varphi^n + b_0 (-\varphi^{-1})^n$$. 
However, the same conclusion can be drawn anywhere else we can identify a solution space as the kernel of an endomorphism of this 
kind.

## ODEs
Let $$V$$ be the set of smooth functions from $$\mathbb{C}$$ to itself regarded as a $$\mathbb{C}$$ vector space. Then differentiation 
(denoted $$D$$) is an endomorphism of $$V$$, and, the solutions of an ODE are the kernel $$p(D)$$ for some polynomial $$p$$. 
If we can solve simple linear ODEs, then we will understand the solutions of all ODEs with separable characteristic polynomials. 
The ODE $$y^\prime = \lambda y$$ has solution $$y = Ce^{\lambda x}$$. 

**Corollary (3)**. 
The solutions of an ODE with separable characteristic polynomial $$p(z) = (z - \lambda_1)(z-\lambda_2)\cdots(z-\lambda_n)$$ are 

$$
\begin{equation*}
    y = \sum_{i=1}^n C_i e^{\lambda_i x}
\end{equation*}
$$

Powerful stuff. Of course if we can solve powers of linear factors then we are done entirely. Fortunately we can. Viz the 
Leibnitz rule;

$$
\begin{align*}
    D^n(ye^{-\lambda x}) = (D - \lambda I)^n(y)
\end{align*}
$$

Therefore, the solutions are precisely the solutions of 

$$
\begin{align*}
    D^n(ye^{-\lambda x}) &= 0 \\
    y &= (a_0 + a_1 x + \cdots a_{n-1}x^{n-1})e^{\lambda x}
\end{align*}
$$

**Corollary (4)**. 
The solutions of an ODE with characteristic polynomial $$p(z) = (z - \lambda_1)^{m_1}(z-\lambda_2)^{m_2}\cdots(z-\lambda_n)^{m_n}$$ are 

$$
\begin{equation*}
    y = \sum_{i=1}^n f_i(x) e^{\lambda_i x}
\end{equation*}
$$

where $$f_i(x)$$ is a polynomial of degree $$m_i - 1$$. 
I'll end this post here, but we will see in the next post that the technique above generalises. In the exercises we'll see that this 
technique is applicable to our work with sequences also.

# Exercises

Our proof of Corollary 4 isn't as straightforward for sequences because the shift operator does not satisfy the Leibniz rule. It is however 
related to a kind of differentiation. Throughout we will regard $$A = F^\mathbb{N}$$ as an $$F$$ algebra with the multiplication as convolution. I.e. 
$$(a_n)(b_n) = c_n$$, where $$c_n = \sum_{k=0}^n a_kb_{n-k}$$

1. Show that multiplication of $$A$$ is commutative and associative. I won't judge if you decide to take the latter on faith, it is a little tedious. 
Show that every sequence $$a_n \in A$$ is invertible if $$a_0 \neq 0$$.

2. Define the finite difference operator so that $$\Delta a_n = b_n$$ where $$b_n = a_{n+1} - a_n$$. Show that the finite difference operator 
satisfies the Leibnitz rule for differentiation.

3. Show that for any $$\lambda \in F$$, there is an invertible $$\lambda$$ eigenvector of the finite difference operator in $$A$$.

4. Let $$v$$ be a $$1 - \lambda$$ eigenvector of the finite difference operator. Show that 
$$
\begin{equation*}
    \Delta^n(a_n v) = (T -\lambda I)^n(a)v
\end{equation*}
$$

5. Show by induction that $$\ker(\Delta^n)$$ is the subspace of polynomials in $$n$$ of degree $$n-1$$ or fewer. 

6. State and prove an analog of corollary 4 for $$A$$.
