---
title: "Newman's Machine"
date: 2024-05-17
permalink: /posts/2024/05/17/Newmans-Machine/
tags:
  - Number Theory
  - Prime Number Theorem
  - Analytic Number Theory
comments: true
layout: single
---

# Abstract
In a famous [paper](https://people.mpim-bonn.mpg.de/zagier/files/doi/10.2307/2975232/fulltext.pdf) Zagier presents a short proof 
of the Prime Number Theorem largely due to Newman. The mechanism of the proof is in principle capable of efficiently deriving 
asymptotics for the partial sums of many interesting sequences. In this post I prove (modulo some exercies) a theorem which makes 
this process routine, and demonstrate its use with a number of applications.

## Assumed Knowledge
The proof of this theorem will involve some light complex analysis and its applications will draw from the theory of convolutions in elementary number theory. 
I will also make use of some asymptotic notation. In particular one writes $$f(x) = O(g(x))$$ if there exists a positive constant $$C$$ such that $$|f(x)| \leq g(x)$$, 
$$f(x) \sim g(x)$$ if $$\lim_{x\to\infty}f(x)/g(x) = 1$$, and $$f(x) = o(g(x))$$ if $$\lim_{x\to\infty}f(x)/g(x) = 0$$.

# Newman's Machine

**Newman's Machine**: Suppose $$a_n$$ is a sequence of positive real numbers with partial sums $$A(x) = \sum_{n\leq x}a_n$$, and:
1. The dirichlet series $$L(s, a) = \sum_{n=1}^\infty a_n n^{-s}$$ is convergent for $$\Re(s) > \sigma > 0$$. 
2. $$L(s, a)$$ extends holomorphically to $$\Re(s) \geq \sigma /\{\sigma\}$$ 
3. $$A(x) = O(x^\sigma)$$.

Let $$C$$ be the residue of $$L(s, a)/s$$ at $$s = \sigma$$. Then $$A(x) \sim Cx^\sigma$$ if $$C$$ is positive and $$A(x) = o(x^\sigma)$$ otherwise. 
 
Before we embark on a proof, we offer up an interesting application. We will seek to understand the partial sums of the Euler Totient Function; 

We begin with a trivial bound on $$\varphi$$,  namely $$\varphi(n) \leq n$$. It follows that 

$$
\begin{equation*}
    L(s, \varphi) \leq \sum_{n=1}^\infty \frac{n}{n^s} \leq \zeta(s-1)
\end{equation*}
$$

Because $$\zeta(s-1)$$ converges absolutely for $$\Re(s) > 2$$, the condition is satisfied on taking $$\sigma = 2$$. We will see stronger evidence 
for this choice when we derive an exact analytic continuation in terms of the Zeta function. To that end, we recall the following identity due to Gauss.

$$
\begin{equation*}
    \sum_{d\mid n} \varphi(d) = n
\end{equation*}
$$

It follows that for $$\Re(s) > 2$$,

$$
\begin{align*}
    L(s, \varphi)\zeta(s) &= \zeta(s-1) \\
    L(s, \varphi) &= \frac{\zeta(s-1)}{\zeta(s)}
\end{align*}
$$

Because $$\zeta(s)$$ extends easily to $$\Re(s) > 0$$ except for a pole at $$s = 0$$, $$\zeta(s-1)/\zeta(s)$$ extends $$L(s, \varphi)$$ holomorphically to 
$$\Re(s) \geq 2 > 1$$ except for $$s = 2$$ where the numerator has a pole. It is of course possible to extend Zeta to the entire complex plane except for its pole at $$s = 1$$ but this 
is considerably more involved. We should mention also that Zeta has no zeros in this region to preclude the possibility of poles due to the denominator, this is an easy consequence of its Euler product. 

Let $$\Phi(x) = \sum_{n\leq x} \varphi(n)$$. To finish satisfying the hypotheses of the theorem, we are required to show that $$\Phi(x) = O(x^2)$$, but by our bound on 
$$\varphi$$ it is clear that $$\Phi(x) \leq x^2$$. 

Now we are free to collect on the consequence of the theorem. Because $$\zeta(s-1)$$ has a simple pole with residue $$1$$ at $$s=2$$, 

$$
\begin{equation*}
    C = \frac{1}{2\zeta(2)} = \frac{3}{\pi^2}
\end{equation*}
$$

Finally; $$\Phi(x) \sim \frac{3}{\pi^2}x^2$$.

# Proof

Hopefully your interest is suitably piqued. We sketch a proof of the theorem now. A lengthier proof will be available in my monograph on the topic. 

First, by Abel's lemma (Exercise 1); 

$$
\begin{equation*}
  \sum_{n\leq x}a_n n^{-s} = \frac{A(x)}{x^s} + s\int_1^x \frac{A(t)}{t^{s+1}}dt
\end{equation*} 
$$

Hence, for $$s$$ with $$\Re(s) > \sigma$$, it follows from the fact that $$A(x) = O(x^\sigma)$$ that 

$$
\begin{align*}
  \sum_{n=1}^\infty a_n n^{-s} &= s\int_1^\infty \frac{A(x)}{x^{s+1}}dt \\ 
  \frac{L(s, a)}{s} &= \int_1^\infty \frac{A(x)}{x^{s+1}}dt
\end{align*} 
$$

Write 

$$
\begin{equation*}
  F(s) = \frac{L(s+\sigma, a)}{s+\sigma} - \frac{C}{s}
\end{equation*}
$$

By construction, $$F(s)$$ is holomorphic for $$\Re(s) \geq 0$$. For $\Re(s) > 0$, we have 

$$
\begin{equation*}
  F(s) = \int_{}
\end{equation*}
$$