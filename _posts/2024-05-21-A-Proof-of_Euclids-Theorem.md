---
title: "A Proof of Euclid's Theorem"
date: 2024-05-21
permalink: /posts/2024/05/21/A-Proof-of-Euclids-Theorem/
tags:
  - Number Theory
  - Euclid's Theorem
  - Analytic Number Theory
comments: true
layout: single
---

This my proof of Euclid's Theorem. There are many like it, but this one is mine. 

# Abstract
I'm preparing a rather long post on a generalisation of the proof mechanism in Zagier's Paper on Newman's 
Short Proof of the Prime Number Theorem. Since it may not be ready for a week, here's a short post about 
one approach to the weakest theorem in this direction. I was dismayed if unsurprised to learn that it's essentially 
a worse version of a proof due to Erd&#x151;s.

# The Proof
The basic idea is this, every positive integer has its own prime factorisation and we therefore require 
an increasing supply of primes to generate unique combinations. 

Suppose there are exactly $$\Pi$$ primes. Then, for every integer $$n \leq N$$, there is a unique prime factorisation 
of the form $$p_1^{a_1} \cdots p_\Pi^{a_\Pi}$$. Taking logarithms, 

$$
\begin{equation*}
    a_1 \log p_1 + ... + a_\Pi \log p_\Pi = \log n \leq \log N
\end{equation*}
$$

Because every number at most $$N$$ admits exactly one such factorisation, simple estimates on the number of tuples which satisfy 
this bound will grant our conclusion. In particular; 

$$
\begin{equation*}
    a_1 + ... + a_\Pi \leq \frac{\log N}{\log 2}
\end{equation*}
$$

Taking $$C = \lfloor\frac{\log N}{\log 2}\rfloor$$ it follows by a standard combinatorial argument that the number of tuples is bounded from above by 
$$\binom{C + \Pi}{\Pi} \leq C^\Pi \leq \left(\frac{\log N}{\log 2} \right)^\Pi$$. This is clearly dominated by large $$N$$, 
but there must be $$N$$ unique prime factorisations. 
