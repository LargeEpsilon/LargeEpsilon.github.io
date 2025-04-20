---
title: "Linear Recurrences 101"
date: 2025-04-12
permalink: /posts/2025/04/12/Linear-Recurrences-101
tags:
  - Generating Functions 
  - Linear Recurrences
  - Fibonnaci Numbers
comments: true
layout: single
---

# Introduction
This post is something of a PSA and its introduction will be a little technical, but I will 
present as much of the body as possible without assuming any particular background of the reader.
Most students at some point learn that if a linear recurrence has a separable 
characteristic polynomial, then its solution is a linear combination of exponentials of its roots. 
It has not been my experience that this result is generalised in a standard undergraduate curriculum. 
This is surprising because the theory is rather pretty and it is not too difficult to do so. 
In this post we will describe the solutions completely. 

# Prerequisites
To get absolutely everything out of this post it will be best to have some grounding in algebra, linear and 
abstract. The Chinese Remainder Theorem for PIDs in particular will play a significant role in justifying a 
central claim, but some familiarity with partial fraction decomposition will be more than sufficient here. 

# The Fibonacci Numbers
I was very surprised to learn that the Fibonacci numbers have a closed form solution. Unfortunately, the result 
was first presented to me as an exercise in diagonalisation in a Linear Algebra class. This is certainly a neat 
application of diagonalisation, and we will revisit something like this view in a follow up, but it renders certain things opaque. Enough 
commentary for now, let's define the Fibonnaci numbers and take a look at the formula. Let $$F_0 = 0$$, $$F_1 = 1$$. 
For $$n \geq 2$$, let $$F_n = F_{n-1} + F_{n-2}$$. Then 

$$
\begin{equation*}
    F_n = \frac{1}{\sqrt{5}}\varphi^{n} - \frac{1}{\sqrt{5}}(-\varphi^{-1})^n
\end{equation*}
$$

where $$\varphi$$ is the positive root of the polynomial $$p(x) = x^2 - x - 1$$. I deliberately choose to define the 
golden ratio like so, and it is in fact well defined, since; the discriminant of $$p$$ is positive, and therefore it has 
two distinct real roots, and, the product of its roots is $$-1$$, and therefore exactly one of them is positive. 
As a corollary, we know that the other root is $$-\varphi^{-1}$$. I want to draw your attention to a couple of 
coincedences. The recurrence defining $$F_n$$ may be written as $$F_n - F_{n-1} - F_{n-2} = 0$$, which 
mirrors $$p$$, and the powers that appear in the formula for $$F_n$$ are precisely 
the roots of $$p$$. Curious! It is not difficult to verify such a formula inductively. Since 
we have two degrees of freedom in choosing the coefficients of $$\varphi^n$$ and $$(-\varphi^{-1})^n$$, I will ask you to either verify yourself or take 
it on faith that the formula holds for $$n=0,1$$. Otherwise, suppose the result is true for all $$n < m$$ for some 
$$m \geq 2$$. Then;

$$
\begin{align*}
  F_m &= F_{m-1} + F_{m-2} \\
  &= \frac{1}{\sqrt{5}}\left(\varphi^{m-1} + \varphi^{m-2}\right) - \frac{1}{\sqrt{5}}\left((-\varphi^{-1})^{m-1} + (-\varphi^{-1})^{m-2}\right) \\
  &= \frac{1}{\sqrt{5}}\varphi^{m-2}\left(\varphi + 1\right) - \frac{1}{\sqrt{5}} (-\varphi^{-1})^{m-2}\left((-\varphi^{-1}) + 1\right) \\
\end{align*}
$$

Now, precisely because of $$\varphi$$'s definition, we see that $$\varphi^2 = \varphi + 1$$. Similarly, 
$$(-\varphi^{-1})^2 = -\varphi^{-1} + 1$$. Hence;

$$
\begin{align*}
  F_m &= \frac{1}{\sqrt{5}}\varphi^{m-2}\varphi^2 - \frac{1}{\sqrt{5}} (-\varphi^{-1})^{m-2}(-\varphi^{-1})^2 \\
  &= \frac{1}{\sqrt{5}}\varphi^m - \frac{1}{\sqrt{5}} (-\varphi^{-1})^m
\end{align*}
$$

Why was this possible? Well first of all it was rather convenient that there were exactly two roots of this polynomial. 
Recall that I brushed aside concerns about verifying the formula for $$n=0, 1$$. We cannot use the recurrence to verify 
the formula in these cases, but we can certainly hope that the pair of equations

$$
\begin{align*}
  A + B &= F_0 \\
  A\varphi + B(-\varphi^{-1}) &= F_1
\end{align*}
$$

has a solution. Two equations to satisfy, two coefficients to solve for. Secondly, the roots we put forward satisfy 
a recurrence of powers matching the form of the recurrence we used to define the Fibonacci numbers. 

 In what follows we consider 
a general field $$F$$, but in most cases we will be interested in either the field of rational numbers or the field 
of real numbers, both of which have algebraic closure $$\mathbb{C}$$.


**Definition (1).** Let $$F$$ be a field, $$k$$ an integer, and let $$a_n$$ be a sequence defined recursively like so;

 - $$a_i \in F$$ are prescribed constants for $$i < k$$. 

 - $$a_n = c_1a_{n-1} + c_2a_{n-2} + ... + c_k a_{n-k}$$ for $$n \geq k$$ and constants $$c_i \in F$$.

 Then we say $$a_n$$ is a linear recurrence of order $$k$$, with characteristic polynomial;

$$
\begin{equation*}
    p(x) = x^k - \sum_{t=1}^k c_{t}x^{k-t} = x^k - c_1 x^{k-1} - c_2 x^{k-2} - ... - c_k
\end{equation*}
$$

**Remark**. The characteristic polynomial always has non zero constant term, and therefore zero is never a root 
of the characteristic polynomial.

With these definitions we can state and prove a simple theorem about linear recurrences. 

**Theorem (2).** Let $$a_n$$ be a linear recurrence of order $$k$$ with a separable characteristic polynomial (i.e. 
every root of $$p$$ has multiplicity 1.), and let $$\lambda_1, \lambda_2, ..., \lambda_k$$ be the roots of the 
polynomial over the algebraic closure $$K$$ of $$F$$. Then there are constants $$q_1, ..., q_k \in K$$ such that 


$$
\begin{equation*}
a_n = \sum_{s=1}^k q_s \lambda_s^n =  q_1 r_1^n + q_2r_2^{n} + ... + q_k r_k^n
\end{equation*}
$$

**Remark**. Because the first $$k$$ terms of the sequence are in $$F$$, we see that every term of the sequence 
is in $$F$$ despite the fact that neither the $$q_i$$ nor the $$\lambda_i$$ necessarily are.

**Proof of Theorem (2)**. 

First we note that because each $$\lambda_s$$ is a root of $$p$$, 

$$
\begin{equation*}
    \lambda_s^k = \sum_{t=1}^k c_t \lambda_s^{k-t},
\end{equation*}
$$

we will need this fact later. 

If such $$q_i$$ exist, they are at least partially determined by the equations 

$$
\begin{equation}
  q_1 \lambda_1^i + q_2 \lambda_2^i + ... + q_k \lambda_k^i = a_i
\end{equation}
$$

for $$0 \leq i < k$$. This gives rise to the matrix equation $$MQ = A$$, where $$Q$$ is the column vector of the 
$$q_i$$, $$A$$ is the column vector of the $$a_i$$, and 

$$
\begin{equation*}
  M = \begin{bmatrix}
    1 & 1 & \cdots & 1 \\
    \lambda_1 & \lambda_2 & \cdots & \lambda_k \\
    \lambda_1^2 & \lambda_2^2 & \cdots & \lambda_k^2 \\
    \vdots & \vdots & \ddots & \vdots \\
    \lambda_1^{k-1} & \lambda_2^{k-1} & \cdots & \lambda_k^{k-1}
    \end{bmatrix} 
\end{equation*}
$$

$$M$$ is a Vandermonde matrix, and it is an interesting object in its own right. Its determinant is given 
by the formula

$$
\begin{equation*}
  \det(M) = \prod_{1\leq i\leq j \leq k}(\lambda_i - \lambda_j).
\end{equation*}
$$

A proof of this fact will be assigned as an exercise. Importantly, this formula guarantees that the determinant is 
non zero if the $$\lambda_i$$ are all distinct. Because the characteristic polynomial is separable, we know this to 
be true. It follows that there is a unique solution $$Q$$ satisfying the initial conditions $$a_i$$ for 
$$0 \leq i < k-1$$. Then, by induction;

$$
\begin{align*}
    a_n &= \sum_{t=1}^k c_ta_{n-t} \\
    &= \sum_{t=1}^k c_t \sum_{s=1}^k q_s \lambda_s^{n-t} \\
    &= \sum_{s=1}^k q_s \lambda^{n-k}\sum_{t=1}^k c_t\lambda^{k-t} \\
    &= \sum_{s=1}^k q_s \lambda^n
\end{align*}
$$

As desired $$\square$$. 

Great, we now completely understand the solutions of linear recurrences with separable characteristic polynomials. 
Unfortunately, the determinant of $$M$$ suggests that this approach is unlikely to work for polynomials with 
repeated roots. In particular, the determinant will be $$0$$ if we include the roots repeatedly, or there will 
be too few coefficients if we only include each root exactly once regardless of multiplicity. Let's change tack.

# Generating Functions
A useful technique for studying sequences which satify additive recursive identities is to encode them as 
generating functions. We say that 

$$
\begin{equation*}
    g(z) := \sum_{n=0}^\infty a_n z^n = a_0 + a_1 z + a_2 z^2 + ....
\end{equation*}
$$

is the generating function of $$a_n$$. Formally, the generating function is an algebraic object, not a function 
to be evaluated subject to troublesome questions of convergence. We say that $$g(z)$$ belongs to 
the ring of formal power series $$F[[z]]$$. This ring satisfies certain properties if $$F$$ is a field:

- It's a PID,
- Its units are the polynomials with non zero constant coefficient.

The former is a somewhat technical condition we'll stow away for later, the latter says that $$1/g(z)$$ is also 
an element of the ring if the constant term of $$g(z)$$ is non zero. What does $$g$$ have to offer us?

Let's take $$g(z)$$ to be the generating function of the Fibonacci numbers and suspend questions of motivation 
for a moment.

$$
\begin{align*}
  g(z) - zg(z) - z^2g(z) &= -z \\
  g(z) &= \frac{-z}{1 - z - z^2} \\
  g(z) &= \frac{1}{\sqrt{5}}\frac{1}{1-\varphi z} - \frac{1}{\sqrt{5}}\frac{1}{1 - (-\varphi^{-1})z}
\end{align*}
$$

verfying the first and last lines is left as an exercise. 
Earlier we said that every polynomial with non zero constant coefficient is a unit. Then 
$$(1-\varphi z)$$ and $$(1 - (-\varphi^{-1})z)$$ are units. In fact;

$$
\begin{equation*}
  \frac{1}{1-\varphi z} = \sum_{n=0}^\infty \varphi^{n}z^n
\end{equation*}
$$

and 

$$
\begin{equation*}
  \frac{1}{1-(-\varphi^{-1}) z} = \sum_{n=0}^\infty (-\varphi^{-1})z^n.
\end{equation*}
$$

These are of course geometric series, but this is an algebraic statement not an analytic one. You should verify algebraically that 

$$
\begin{equation*}
  (1-\varphi z) \sum_{n=0}^\infty \varphi^{n}z^n = 1.
\end{equation*}
$$

Therefore, we recover

$$
\begin{equation*}
  g(z) = \sum_{n=0}^\infty \left(\frac{1}{\sqrt{5}}\varphi^n + \frac{1}{\sqrt{5}}(-\varphi^{-1})^n\right)z^n
\end{equation*}
$$

that is, $$F_n = (\varphi^n + (-\varphi^{-1})^n))/\sqrt{5}$$.

Now I probably owe some explanations. Why $$g(z)(1 - z - z^2)$$?

A nice property of generating functions is that 

$$
\begin{equation*}
    z^t g(z) = \sum_{n=0}^\infty z^{n+t}a_n = \sum_{n=k}^\infty z^n a_{n-t} + \sum_{n=0}^{k-t-1}z^{n+t} a_{n}.
\end{equation*}
$$

That is, multiplying $$g(z)$$ by $$z^t$$ has the effect of shifting the coefficients of the generating function up to 
some finite of number of residual terms. From this we deduce that 

$$
\begin{align*}
  g(z) - zg(z) - z^2g(z) &= \sum_{n=2}^\infty z^n(F_n - F_{n-1} - F_{n-2})z^n - z \\
  g(z)(1 - z - z^2) &= -z
\end{align*}
$$

That answers some questions, but in what way is $$1 - z - z^2$$ related to $$p(z) = z^2 - z - 1$$? The concise 
answer is $$1 - z - z^2 = z^2 p(1/z)$$. The following lemma clarifies the importance of this relationship.

**Lemma (3)**. If $$p(z)$$ is a polynomial of degree $$k$$ of which $$0$$ is not a root, then  
$$z^kp(z^{-1})$$ is a polynomial whose roots are the reciprocals of those of $$p(z)$$. If $$p(z)$$ is monic 
with roots $$\lambda_1, ..., \lambda_k$$, then 

$$
\begin{equation}
    z^{k}p(z^{-1}) = (-1)^k \prod_{s=1}^k (1-\lambda_s z)
\end{equation}
$$

**Proof of Lemma (3)**. Exercise.

$$(1-z-z^2) = (1-\varphi z)(1-(-\varphi^{-1})z)$$ is an immediate consequence of Lemma (3). Finally, 
partial fraction decomposition carries us the last step of the way. In particular, we expect that there 
are coefficients $$A$$ and $$B$$ such that

$$
\begin{equation*}
  \frac{-z}{1-z-z^2} = \frac{A}{1-\varphi z} + \frac{B}{1 - (-\varphi^{-1})z}.
\end{equation*}
$$

In fact, we deduce the following simultaneous equations for $$A$$ and $$B$$ by comparing 
coefficients;

$$
\begin{align*}
  A + B &= 0 = F_0 \\
  A\varphi + B(-\varphi^{-1}) z &= 1 = F_1
\end{align*}
$$

we have been here before, and this seems like a lot of effort to recover the same results as last time. The 
difference is that partial decomposition is still valid when the denominator has repeated roots! Let's recap 
how we got here by reproving Theorem (2) by way of generating functions.

**Proof of Theorem (2)**.

Let $$g(z)$$ be the generating function of a linear reccurence $$a_n$$ of order $$k$$ with characteristic 
polynomial $$p(z)$$. Take $$r_t(z) = c_t\sum_{n=0}^{k-t-1} z^{n+t}a_n$$ for $$t < k$$, $$r(z) = \sum_{t=1}^{k-1}r_t(z)$$. 
Note that $$r(z)$$ is a polynomial of degree less than $$k$$.
Then as we have seen previously

$$
\begin{align*}
    g(z) - \sum_{t=1}^{k} c_tz^t g(z) &= \sum_{n=k}^\infty \left(a_n - \sum_{t=1}^k c_ta_{n-t}\right)z^n  + r(z) \\
    g(z)z^kp(z^{-1}) &= r(z) \\
    g(z) &= \frac{r(z)}{z^kp(z^{-1})} \\
    g(z) &= \frac{r(z)}{\prod_{s=1}^k (1 - \lambda_s z)}
\end{align*}
$$

Now, we would like to know that there are coefficients $$q_i$$ such that 

$$
\begin{equation*}
    \frac{r(z)}{\prod_{s=1}^k (1 - \lambda_s z)} = \sum_{s=1}^k \frac{q_s}{1 - \lambda_s z}
\end{equation*}
$$

In essence we saw a proof of this fact viz the determinant of the Vandermonde matrix in the first proof of this 
theorem. Here I will ask that you appeal either to a nostalgic faith in partial fraction decomposition, or, 
the following application of the Chinese Remainder Theorem. I conclude the proof here. $$\square$$.

**Corollary (5) (of the Chinese Remainder Theorem)** 
Let $$p_i(z)$$ be pairwise coprime polynomials in $$F[z]$$ and $$r(z)$$ a polynomial 
with $$\deg(r(z)) < \sum_{i}\deg(p_i(z))$$, and let $$q_i(z)$$ be the remainder of the quotient $$r(z)/p_i(z)$$. 
Then;

$$
\begin{equation*}
    \frac{r(z)}{\prod_i p_i(z)} = \sum_{i} \frac{q_i(z)}{p_i(z)}
\end{equation*}
$$

That is, one can always find a partial fraction decomposition of a quotient of polynomials if the denominator is grouped 
into factors which do not share roots. There is a fair deal of work involved in establishing this fact, but I have 
prepared a series of guided exercises for the inclined reader.

We have now verified completely (up to a belief in the Chinese Remainder Theorem) the generating function based 
proof of Theorem (2). However, we have also largely prepared ourselves for dealing with the case where the 
characteristic polynomial is not separable. We are now ready to state our main theorem. 

**Theorem (8)** Let $$a_n$$ be a linear recurrence of order $$k$$ and characterstic polynomial $$p(z)$$ and 
let $$g(z)$$ be the generating function of $$a_n$$. Let $$\lambda_1, \lambda_2, ... \lambda_l$$ be the roots 
of $$p(z)$$ with multiplicities $$m_1, m_2, ..., m_l$$.  
Then there exist $$q_{i,j}$$ for $$1\leq i \leq l$$, $$1\leq j \leq m_i$$ with $$q_{i, m_i} \neq 0$$  such that 

$$
\begin{equation*}
  g(z) = \sum_{i=1}^l \sum_{j=1}^{m_l} \frac{q_{i,j}}{(1-\lambda_i z)^j}
\end{equation*}
$$

**Proof of Theorem (8)**. 

Taking $$r(z)$$ as in the proof of Theorem (2), we recover immediately that 

$$
\begin{equation*}
    g(z) = \frac{r(z)}{\prod_{i=1}^l (1-\lambda_i z)^m_i}
\end{equation*}
$$

The $$(1-\lambda_i z)^{m_i}$$ clearly do not share roots. Therefore, 
by Corollary (5) of the Chinese Remainder Theorem, there exist polynomials $$q_i(z)$$ such that

$$
\begin{equation*}
    g(z) = \sum_{i=1}^l \frac{q_i(z)}{(1-\lambda_i z)^{m_i}}.
\end{equation*}
$$

Finally, by simple polynomial long division, for each $$i$$ there exist constants $$q_{i,j}$$ 
with $$q_{i, m_i} \neq 0$$ such that 

$$
\begin{equation*}
    \frac{q_i(z)}{(1-\lambda_i z)^{m_i}} = \sum_{j=1}^{m_i} \frac{q_{i, j}}{(1-\lambda_i z)^j}
\end{equation*}
$$

This proves the theorem $$\square$$.

We said this was the main theorem, and in a way it is, but it's not quite as satisfying as Theorem (2) 
because we don't necessarily know what to make of $$q_{i,j}(1-\lambda_i z)^{-j}$$ for $$j > 1$$. Of 
course in the case $$j = 1$$ we know precisely what generating function this corresponds to. Fortunately, 
there is a sensible way to interpret powers of generating functions. 

**Lemma (9)**. 
Let $$g(z) = \sum_{n=1}^\infty a_n z^n$$. Then;

$$
\begin{equation*}
    (g(z))^j = \sum_{n=0}^\infty \left(\sum_{t_1 + t_2 + ... + t_j = n}a_{t_1}a_{t_2}\cdots a_{t_j}\right)z^n
\end{equation*}
$$

**Proof (9)**. Exercise.

**Corollary (10)**. 

$$ 
\begin{equation*}
    \frac{1}{(1-\lambda z)^j} = \sum_{n=0}^\infty \lambda^n \binom{n+j-1}{j-1}z^n
\end{equation*}
$$

**Proof of Corollary (10)**. 

In view of Lemma (9)

$$
\begin{align*}
    \frac{1}{(1-\lambda z)^j} &= \sum_{n=0}^\infty \left(\sum_{t_1 + t_2 + ... t_j = n}\lambda^{t_1}\lambda^{t_2}\cdots \lambda^{t_j}\right)z^n \\
    &= \sum_{n=0}^\infty \left(\sum_{t_1 + t_2 + ... t_j = n}1\right)\lambda^nz^n
\end{align*}
$$

The number of ordered partitions of $$n$$ with $$j$$ parts is exactly $$\binom{n+j-1}{j-1}$$ (exercise. Hint: consider the number of ways to arrange $$n$$ objects with 
$$j-1$$ partitions). 
The result follows. $$\square$$.

Now, because $$j$$ is fixed over the sum, we see that 

$$
\begin{align*}
    \binom{n + j - 1}{j-1} &= \frac{(n+j-1)(n+j-2)\cdots (n+1)}{(j-1)!} \\
    &= f_j(n)
\end{align*}
$$

for some fixed polynomial $$f_j$$ with degree $$j-1$$. Therefore;

**Corollary (11)**. 
Let $$a_n$$ be a recurrence of order $$k$$ with ...

Then there exist constants $$q_i$$ and polynomials $$f_i \in \mathbb{F}[n]$$, $$1 \leq i \leq l$$, with $$\deg(f_i) = m_i - 1$$ such that 

$$
\begin{equation*} 
    a_n = \sum_{i=1}^l f_i(n)\lambda_i^{n}.
\end{equation*}
$$

**Remark**. This solves linear recurrences completely since we can construct the $$f_i$$ explicitly.

**Proof of Corollary (11)**. This is an immediate consequence of Corollary (10) applied to Theorem (8).


# Exercises
This set of exercises is aimed at establishing Corollary 5. All polynomials are taken over $$F[z]$$, and we will say 
that polynomials $$p,q$$ are coprime if they do not share roots over the algebraic closure of $$F$$. Feel free to interpret $$F$$ as either 
$$\mathbb{Q}$$, $$\mathbb{R}$$ or $$\mathbb{C}$$ if you aren't familiar with fields. The algebraic closure of all of these 
is $$\mathbb{C}$$.

1. Suppose $$p, q$$ share a root in the algebric closure of 
$$F$$. Show that any linear combination of $$p, q$$ over $$F$$ also shares this root.

2. Show that if $$p, q$$ are coprime, then any linear combination is also coprime with each of 
$$p, q$$.

3. Show by induction on $$\deg(p) + \deg(q)$$ that for coprime polynomials $$p, q$$  
there exist polynomials $$u, v$$ such that 
$$pu + qv = 1$$. Hint, construct a linear combination over $$F$$ which has smaller degree.

4. Suppose $$p$$ has degree at least $$1$$, and suppose $$p, q$$ are coprime. Show that if 
$$p$$ divides $$aq$$, then $$p$$ divides $$a$$.

5. Suppose that $$p, q$$ are coprime. Show that $$x$$ is divisible by $$pq$$ iff 
$$x$$ is divisible by $$p$$ and $$x$$ is divisible by $$q$$. Hint, one direction is trivial, 
for the other, invoke 3 then multiply by $$x$$.

6. Let $$f_p, f_q, p, q$$ be polynomials such that $$p, q$$ do not share roots. Suppose 
    $$x - f_p$$ is divisible by $$p$$, and $$x - f_q$$ is divisible by $$q$$. 
    Show that there is a solution. Show that this solution is unique modulo $$pq$$ in 
    the sense that for any two solutions $$x, x^\prime$$, $$x - x^\prime$$ is divisible by 
    $$pq$$. Hint, invoke the result of (3) directly to find a solution, use (5) to show 
    uniqueness.

7. Induct on 6 to show the result for $$f_{p_1}, f_{p_2}, ..., f_{p_n}, p_1, p_2, ..., p_{n}$$ where 
none of the $$p_i$$ share roots.

8. Prove corollary (5). You will need the fact that $$\deg(r) < k$$.
