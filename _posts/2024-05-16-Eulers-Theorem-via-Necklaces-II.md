---
title: "Euler's Theorem via Necklaces II"
date: 2024-05-16
permalink: /posts/2024/05/16/Eulers-Theorem-via-Necklaces-II/
tags:
  - Number Theory
  - Combinatorics
comments: true
layout: single
---

# Abstract
In the [previous post](https://largeepsilon.github.io/posts/2024/05/16/Eulers-Theorem-via-Necklaces-I/) a combinatorial proof of Fermat's little theorem (FLT)
was given, with the claim that it would be extended to a proof of the (almost) more general Euler's Theorem. In this post we make good on that promise, 


## Assumed Knowledge
We will assume that the reader is familiar with the M&ouml;bius Function $$\mu$$, the M&ouml;bius Inversion Formula, a certain strengthening of Euclid's Lemma, 
the multiplicativity of the Euler Totient Function $$\varphi$$, and the Chinese Remainder Theorem. Exercises are provided at the end to walk the inclined 
reader through these prerequisites.

**The M&ouml;bius Function**: Define the M&ouml;bius function $$\mu(n)$$ like so;

$$
\begin{equation*}
    \mu(n) = 
    \begin{cases}
        0 & n \text { is divisible by the square of a prime} \\
        (-1)^k & n \text { is the product of } k \text{ distinct primes}
    \end{cases}
\end{equation*}
$$

**The M&ouml;bius Inversion Formula**: Suppose $$f, g: \mathbb{N} \to \mathbb{C}$$ are arithmetical functions with;

$$
\begin{equation*}
    g(n) = \sum_{d|n}f(d) 
\end{equation*}
$$


Then;

$$
\begin{equation*}
    f(n) = \sum_{d|n}\mu(d)g\left(\frac{n}{d}\right) 
\end{equation*}
$$

**Euclid's Strong Lemma**: If $$n$$ and $$a$$ are relatively prime, and $$n\mid ab$$, then $$n\mid b$$.

**Multiplicativity of $$\varphi$$**: If $$m$$ and $$n$$ are relatively prime, then $$\varphi(mn) = \varphi(m)\varphi(n)$$.

**The Chinese Remainder Theorem**: Suppose $$M_1, M_2,...,M_n$$ are pairwise relatively prime, then the set of congruences 

$$
\begin{equation*}
    x \equiv a_i \mod M_i
\end{equation*}
$$

has a unique solution modulo $$N = M_1M_2\cdots M_n$$.

# Body

Our objective is a proof of Euler's Theorem.

**Euler's Theorem**: If $$a$$ and $$n$$ are relatively prime, then;

$$
\begin{equation*}
    n \mid a^{\varphi(n)} - 1
\end{equation*}
$$

The thrust of the proof of FLT was to count the set of necklaces of length $$p$$ made from $$a$$ different kinds of beads with exactly $$p$$ symmetries. The equivalence 
relation associating necklaces which are rotations of each other then divides the set of necklaces into partitions of size $$p$$. It follows that 
the number of such necklaces is divisible by $$p$$. 


In order to prove Euler's Theorem, we should first count the set of necklaces of length $$n$$ with exactly $$n$$ symmetries, for arbitrary $$n$$. 
Let $$C_a(n)$$ be the number of such necklaces. Then $$n\mid C_a(n)$$ by the same 
partitioning argument used in the proof of FLT. The key observation in counting $$C_a(n)$$ is that if 
a necklace has exactly $$d$$ symmetries, then it has a pattern of length $$d$$ which tiles the necklace. It follows 
that $$d$$ divides $$n$$, and, that the necklace is determined entirely by a pattern of length $$d$$, i.e. the number of such necklaces is 
$$C_a(d)$$. Because there are $$a^n$$ total necklaces, and each of these must have *some* number of symmetries;

$$
\begin{equation*}
    \sum_{d|n}C_a(d) = a^n
\end{equation*}
$$

By the M&ouml;bius Inversion Formula

$$
\begin{equation*}
    C_a(n) = \sum_{d|n}\mu(d) a^{\frac{n}{d}} 
\end{equation*}
$$

We have *a* formula, it is not clear that it is all that useful. Certainly we can't expect that the sum on the right corresponds to 
something like $$a^{\varphi(n)} - 1$$ in the general case. However, convolutions with $$\mu$$ are generally easily understood if $$n$$ 
has a small number of prime divisors. For example, if $$n = p^k$$ for a prime $$p$$, then the summand is only supported for 
$$d = 1$$ and $$d = p$$. The other divisors of $$p^k$$ are divisible by $$p^2$$.

$$
\begin{align*}
    C_a(p^k) &= \mu(1)a^{p^k} + \mu(p)a^{p^{k-1}} \\ 
    &= a^{p^k} - a^{p^{k-1}}\\
    &= a^{p^{k-1}}(a^{p^{k-1}(p-1)} - 1) \\
    &= a^{p^{k-1}}(a^{\varphi(p^k)} - 1)
\end{align*}
$$

if $$p^k$$ is coprime with $$a$$, then it is also coprime with $$a^{p^{k-1}}$$. Because $$p^k\mid C_a(p^k) = a^{p^{k-1}}(a^{\varphi(p^k)} - 1)$$, 
it follows by the strengthed form of Euclid's Lemma that $$p^k \mid a^{\varphi(p^k)} - 1$$. I.e., Euler's theorem for powers of primes. 

Parlaying this partial result into the full proof is 
a standard exercise in the use of the Chinese Remainder Theorem. As usual we stitch the results for prime powers together to handle 
arbitrary $$n$$. Representing $$n$$ by its prime factorisation, $$n = p_1^{m_1}p_2^{m_2} \cdots p_k^{m_k}$$, 
$$\varphi(n) = \varphi(p_1^{m_1})\varphi(p_2^{m_2})\cdots \varphi(p_k^{m_k})$$ by the multiplicativity of $$\varphi$$. 

$$
\begin{align*}
    a^{\varphi(n)} - 1 &= a^{\varphi(p_i^{m_i})(\varphi(n)/\varphi(p_i^{m_i}))} - 1 \\
    &= (a^{\varphi(p_i^{m_i})} - 1)(1 + a^{\varphi(n)/\varphi(p_i^{m_i})} + ... + a^{(\varphi(p_i^{m_i})-1)(\varphi(n)/\varphi(p_i^{m_i}))})
\end{align*}
$$

Therefore, for each element of $$p_i^{m_i}$$ of $$n$$'s prime factorisation, $$p_i^{m_i} \mid a^{\varphi(p^k)}-1 \mid a^{\varphi(n)} - 1$$. That is; 

$$
\begin{equation*}
    a^{\varphi(n)} \equiv 1 \mod p_i^{m_i}
\end{equation*}
$$

Because $$p_i^{m_i} \mid n$$, $$a^{\varphi(n)} \equiv 1 \mod n$$ is a valid solution of the set of congruences above. By the Chinese Remainder Theorem, it is 
the unique solution. Ergo 

$$
\begin{equation*}
    n \mid a^{\varphi(n)} - 1
\end{equation*}
$$

as desired.

# Exercises

1. Define convolution of arithmetical functions like so; 
$$
\begin{equation*}
    (f*g)(n) = \sum_{d\mid n}f(d)g\left(\frac{n}{d}\right)
\end{equation*}
$$
. Show that convolution is associative.

2. Show that $$\sum_{d\mid n}\mu(d)$$ is $$1$$ is $$n=1$$ and $$0$$ otherwise. Hence, prove the mobius inversion formula.

3. Let $$(a, b)$$ be the greatest common divisor of integers $$a$$ and $$b$$. We say that $$a$$ and $$b$$ are coprime or 
relatively prime if $$(a, b) = 1$$. Show by induction that if $$a$$ and $$b$$ are relatively prime, there exist integers 
$$x$$ and $$y$$ such that $$ax + by = 1$$. This result is known as Bezout's Identity. Hint: show that $$(a, b) = (a-b, a)$$.

4. Prove the strong form of Euclid's Lemma. 

5. Use Bezout's identity to prove the existence component of the Chinese Remainder Theorem. We only need the uniqueness, but we're 
already equipped to show the existence. Hint: Show it for two moduli and then induct.

6. Show that if $$a\mid c$$ and $$b\mid c$$ with $$(a, b) = 1$$, then $$ab \mid c$$. Hence Prove the uniqueness component of the Chinese Remainder Theorem.