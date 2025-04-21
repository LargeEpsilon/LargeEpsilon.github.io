---
title: "Making Change is Complex"
date: 2025-01-30
permalink: /posts/2025/01/30/Making-Change-is-Complex
tags:
  - Generating Functions 
  - Complex Analysis
  - Combinatorics
comments: true
layout: single
---

# Abstract 
The change making problem is a computer science classic. However, dynamic programming can only take you so far, and in the limit 
we are left only with analysis. In this post we determine the aymptotics of the number of ways to make change with prescribed 
denominations using methods of complex analysis inspired by the Hardy Littlewood Circle Method. We will make use of generating 
functions, though no prior knowledge of them will be required. Familiarity with asymptotic notation and complex analysis, 
particularly the Laurent Series and the Residue Theorem, will be assumed.

# The Problem
Let $$d_1, d_2, ..., d_m$$ be positive integers denoting the denominations of a particular currency. Let $$C_n$$ be the number 
of ways to represent $$n$$ using these denominations. What is the behaviour of $$c_n$$ as $$n$$ tends to infinity? Is there an 
elementary function $$f$$ such that $$c_n \sim f(n)$$?

# First observations

## Try it out
If you toy with some examples with real denominations, you might notice that you can’t make change for every quantity. In 
Australia, every denomination of coin is divisible by $$5$$ cents. They are; the $$5, 10, 20$$ and $$50$$ cent coins, together 
with the $$1$$ and $$2$$ dollar coins. It follows that any amount we can construct with Australian coins is divisible by $$5$$ 
cents. If we were to divide our denominations by $$5$$, we could construct an equivalent problem in the denominations 
$$1, 2, 4, 10, 20$$ and $$40$$ cents if we were to also divide our targets by $$5$$. Therefore, we will assume that the 
denominations $$d_1, ..., d_m$$ are not all divisible by some non trivial quantity.

## A new denomination
Suppose you devise an entirely accurate and unbelievably efficient algorithm for the problem with Australian coins, only to 
realise you’d forgotten to account for the mysterious $$\$3$$ coin. You’re not necessarily dead in the water. Any representation 
using this set of coins is neatly partitioned into a quantity built from the old set of denominations together with some number 
of the new coins. Let $$c^\prime_n$$ denote the number of ways to represent $$n$$ with only $$\$3$$ coins. We make two 
observations about this arrangement. The first is that

$$
\begin{equation*}
    c^\prime_n = \begin{cases} 
        1 & \$ 3|\$ n \\ 
        0 & \text {else} 
    \end{cases} 
\end{equation*}
$$

More generally, with only a single denomination the number of ways to make change for $$n$$ is exactly $$1$$ if the denomination 
divides that quantity and $$0$$ otherwise. The second is that the total number of ways to make change for $$n$$ is now given by

$$
\begin{equation*} 
    \sum_{t=0}^n c_t c^\prime_{n-t}. 
\end{equation*}
$$

This formula follows naturally on partitioning representations by their sub quantity represented with the old denominations.

# The Generating Function 
You may recognise the preceding formula as the Cauchy Convolution of the sequences $$c$$ and $$c^\prime$$. Otherwise, it should 
at least draw comparison to the product of a pair of polynomials. If we encode the sequences as coefficients of 
‘infinite polynomials’ (formally, elements of the ring of power series $$\mathbb{C}[[z]]$$), then the sequence of their 
convolutions corresponds the the coefficients of the product of these polynomials. Writing 
$$\displaystyle f(z) = \sum_{k=0}^{\infty}c_k z^k$$ and $$\displaystyle g(z) = \sum_{r=0}^\infty c_r^\prime z^r$$. With our 
generating functions we articulate our observations as such (henceforth all quantities implicitly denominated in cents)

$$
\begin{equation*} 
    g(z) = 1 + z^{300} + z^{600} + ... 
\end{equation*}
$$

and,

$$
\begin{equation*} 
    f(z)g(z) = \sum_{n=0}^\infty z^n\sum_{t=0}^n c_t c^\prime_{n-t} 
\end{equation*}
$$

that is, the polynomial which encodes the number of ways to make change with two disjoint sets of denominations is the product 
of the polynomials associated to each set. By considering each polynomial separately, we see that

$$
\begin{equation*} 
    f(z) = \prod_{i=1}^m \left(\sum_{k=0}^\infty z^{d_i k}\right) 
\end{equation*}
$$

The insight of the Hardy Little Wood Circle method to which we will appeal is that such a power series can be shifted to produce 
a Laurent series centered at the origin, whose residue there is any coefficient of $$f(z)$$ we desire. In particular, 
$$z^{-n-1}f(z)$$ regarded as a complex function, if it is meromorphic in a neighbourhood of the origin, has residue $$c_n$$ 
there (recall that the residue of a Laurent series is the coefficient of $$z^{-1}$$).

# Its Analytic Continuation
That the product is meromorphic is easily established. Obviously $$z^{-n-1}$$ is meromorphic on the plane with a pole at zero, 
and $$f(z)$$ is a finite product of geometric series all of which we recall are in fact analytic on the (open) unit disk. In 
fact, $$f(z)$$ is the Mclaurin series expansion of

$$
\begin{equation*} 
    \prod_{i=1}^m \frac{1}{1-z^{d_i}} 
\end{equation*}
$$

which is also meromorphic on the plane, with poles at various roots of unity. We now identify $$f(z)$$ with this product. 
Finally we pass through to the analytic Continuation

$$
\begin{equation*} 
    z^{-n-1}f(z) = z^{-n-1}\prod_{i=1}^m \frac{1}{1-z^{d_i}} 
\end{equation*}
$$

It is easily observed by the residue theorem that the analytic continuation of a meromorphic function shares its residues with 
the function it extends over its domain, so we don’t need to entertain any suspicions that information about the residues is 
distorted by this process. What we gain from this process is the ability to consider integrals of the function 
$$z^{-n-1}f(z)$$ in a much larger domain. Let $$C_R$$ be the circle about the origin with radius $$R > 1$$. Because the poles 
of $$z^{-n-1}f(z)$$ are all contained within the (closed) unit disk, we have by the residue Theorem

$$
\begin{equation*} 
    \frac{1}{2\pi i} \int_{C_R}z^{-n-1}f(z)dz = \text{Res}(z^{-n-1}f(z), 0) + 
    \sum_{\omega\text{, }\omega^{d_i} = 1}\text{Res}(z^{-n-1}f(z), \omega) 
\end{equation*}
$$

For $$n > 1$$, the integrand is certainly $$O(R^{-2})$$ and the length of the path is $$2\pi R$$, from which it follows that 
the integral itself is $$O(1/R)$$ and vanishes in the limit. Together with the observation that 
$$\text{Res}(z^{-n-1}f(z), 0) = c_n$$ we have

$$
\begin{equation*} 
    c_n = -\sum_{\omega\text{, }\omega^{d_i} = 1}\text{Res}(z^{-n-1}f(z), \omega) 
\end{equation*}
$$

Now, if we can only calculate the residues, we have an exact formula!

# Computing Residues
It makes sense to first at least try to understand the nature of the poles. A first cyclotomic observation is that if $$d_i$$ 
and $$d_j$$ are coprime, then the roots, of $$1-z^{d_i}$$ and $$1-z^{d_j}$$ except for $$z=1$$ are disjoint. Though we will see 
eventually that it isn’t necessary, we will assume for now that all pairs $$d_i, d_j$$ are coprime if $$i\neq j$$, rendering 
all poles of $$z^{-n-1}f(z)$$ not at zero or one simple. The formula 

$$
\begin{equation*} 
    \text{Res}(z^{-n-1}f(z), z_0) = \lim_{z\to z_0} z^{-n-1}f(z) 
\end{equation*}
$$

valid when $$z_0$$ is a simple pole of $$z^{-n-1}f(z)$$ makes it clear that the magnitude of the residue is independent of 
$$n$$, ($$|z_0| = 1$$, therefore $$\lim_{z\to z_0}|z|^{-n-1} = 1$$). However, the pole of order $$m$$ at $$z=1$$ is 
inescapable, regardless of the assumptions made on $$m$$ or the $$d_i$$. 
For this we have the more complicated but still standard formula

$$
\begin{equation*} 
    \text{Res}(z^{-n-1}f(z), z_0) = \lim_{z\to z_0} \frac{1}{(m-1)!}\frac{d^{m-1}}{dz^{m-1}}\left[(z-z_0)^m z^{-n-1}f(z)\right]
\end{equation*}
$$

(to see why this is true, write out the Laurent Series and carry out the implied calculations.) The expression being 
differentiated is factored neatly into one component which depends on $$n$$, and one which does not. We write (viz the Leibniz 
formula);

$$
\begin{align*} 
    \frac{d^{m-1}}{dz^{m-1}}\left[(z-z_0)^m z^{-n-1}f(z)\right] &= \sum_{k=0}^{m-1}\binom{m-1}{k}\frac{d^{k}}{dz^{k}}\left[z^{-n-1}\right] \frac{d^{m-1-k}}{dz^{m-1-k}}\left[(z-z_0)^{m}f(z)\right] \\ 
    &= \sum_{k=0}^{m-1}\binom{m-1}{k}(-1)^k(n+1)(n+2)\cdots(n+k)z^{-n-1-k} \frac{d^{m-1-k}}{dz^{m-1-k}}\left[(z-z_0)^{m}f(z)\right] 
\end{align*}
$$

The derivative on the right of the summand is certainly no more responsive to $$n$$ now than it was before its differentiation, and the coefficient of $$z^{-n-1-k}$$ is a polynomial in $$n$$ of degree $$k$$. It follows, that the most significant term comes 
from differentiating $$z^{-n-1}$$ $$m-1$$ times. 

$$
\begin{align*} 
    \frac{d^{m-1}}{dz^{m-1}}\left[(z-z_0)^m z^{-n-1}f(z)\right] &= (-1)^{m-1}(n^{m-1} + p^\prime(n)_{m-1})z^{-n-m} (z-z_0)^m f(z) +\\ 
    & \sum_{k=0}^{m-2}p_{k}(n)z^{-n-1-k}\frac{d^{m-1-k}}{dz^{m-1-k}}\left[(z-z_0)^{m}f(z)\right] 
\end{align*}
$$

where; $$p^\prime_{m-1}$$ is a polynomial of degree $$m-2$$, and for $$0 \leq k \leq m-2$$ $$p_{i}$$ is a polynomial of degree 
$$i$$. In all, regarded as a function of $$n$$;

$$
\begin{equation*} 
    \text{Res}(z^{-n-1}f(z), 1) = \frac{1}{(m-1)!}((-1)^{m-1} n^{m-1} + o(n^{m-1}))\lim_{z\to 1}\left[z^{-n-m}(z-1)^mf(z)\right] + o(n^{m-1}) 
\end{equation*}
$$

If we can compute the limit, we will expect to have captured the most significant part of $$c_n$$. $$z^{-n-m}$$ will dissolve 
harmlessly on taking the limit, as for the remainder; 

$$
\begin{align*} 
    (z-1)^{m}f(z) &= \prod_{i=1}^m \frac{z-1}{1-z^{d_i}} \\ 
    &= \prod_{i=1}^m \frac{(-1)}{1 + z + \cdots + z^{d_i-1}} 
\end{align*}
$$

Finally, it follows that 

$$
\begin{equation*} 
    \lim_{z\to 1}\left[z^{-n-m}(z-1)^mf(z)\right] = \frac{(-1)^m}{d_1 d_2 \cdots d_m} 
\end{equation*}
$$

and hence;

$$
\begin{equation*} 
    \text{Res}(z^{-n-1}f(z), 1) = -\frac{1}{(m-1)!d_1d_2\cdots d_m}(n^{m-1} + o(n^{m-1})) + o(n^{m-1}) 
\end{equation*}
$$

However, precisely the same analysis shows that for poles of lower order, the residue is $$o(n^{m-1})$$. If all the 
denominations possessed a common factor, each term in the product $$f(z)$$ would share a common pole, and its collective order 
would be $$m$$. If this is not the case, we conclude that 

$$
\begin{equation*} 
    c_n = \frac{1}{(m-1)!d_1 d_2\cdots d_m} n^{m-1} + o(n^{m-1}) 
\end{equation*}$$

i.e.,

$$
\begin{equation*} 
    c_n \sim \displaystyle\frac{n^{m-1}}{(m-1)!d_1d_2\cdots d_m} 
\end{equation*}$$
