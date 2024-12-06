---
title: "Euclid's Proof in the Other Direction"
date: 2024-08-31
permalink: /posts/2024/05/21/Euclids-Proof-In-The-Other-Direction/
tags:
  - Number Theory
  - Euclid's Theorem
  - Probabilistic Number Theory
comments: true
layout: single
---

# Abstract 
Euclid's famous proof denies the claim that there are only finitely many primes by looking beyond the product of a finite collection of primes and looking for evidence of primes not considered. In this post I prove that this is not necessary, and show (non constructively) that an integer smaller than the product is in fact not divisible by any of the included primes.

## Pre Requisites
I will make use of some basic ideas and notation from probability theory. I will also invoke the inclusion-exclusion principle as well as a fact from elementary number theory. Proving the former is beyond the scope of this post but I will offer a few words in the way of justification when the time comes, the latter I simply cannot be bothered to prove (nor is it particularly interesting or unituitive).

## Euclid's Proof
I will briefly recount Euclid's proof to frame my result. Suppose there are only finitely many primes $$p_1, p_2, ..., p_n$$. Let $$Q = p_1 p_2 \cdots p_n$$. The observation is that $$Q+1$$ is not divisible by any of the $$p_i$$. Every number larger than one must be divisible by at least one prime, and this divisor of $$Q+1$$ is a counter example. A nice feature of this proof is that it's at least partially constructive. If someone were convinced they had found finite but complete set of the primes, you 
could hunt for a counter example by calculating $$Q+1$$ and looking for its factors. I will prove that there is at least one number smaller than $$Q$$ which will also suffice, but I cannot provide you with an algorithm for computing it, I can only demonstrate that it exists.

## My Proof
My idea is this, I will think about choosing numbers between $$1$$ and $$Q$$ uniformly at random. If I cans how that the probability of choosing a number not divisible by any of the primes $$p_i$$ is non zero, then at least one of the numbers must have this property. 


It is certainly easy enough to determine the probability that a number drawn is not divisible by any particular $$p_i$$. Because $$Q$$ is by definition a multiple of $$p_i$$ exactly $$Q/p_i$$ of the numbers are multiples of $$p_i$$ it follows that the probability that the number is divisible by $$p_i$$ is $$1/p_i$$. The desired probability is its complement, $$1 - 1/p_i$$, but we will have to add a number of these together which may get messy. For now we'll deal with the probability that a chosen number *is* divisible by at least one of the $$p_i$$ and then take the complement. Unfortunately we can't just add together the probabilities and be done with it. For example, the events $$n$$ is divisible by $$p_1$$ and $$n$$ is divisible by $$p_2$$ both include the possibility that $$n$$ is divisible by $$p_1p_2$$, and so we over count many cases in all manner of complicated ways. Fortunately this is a well studied problem, and there is a neat principle called inclusion exclusion which handles it neatly. Let $$D_i$$ be the event that $$n$$ is divisible by $$p_i$$. Then, the principle of inclusion exclusion says;

$$
\begin{align*}
    P(D_1\lor D_2 \lor ... \lor D_n) &= \sum_{1\leq i_1 \leq n}P(D_{i_1}) - \sum_{1\leq i_1 < i_2 \leq n}P(D_{i_1}\land D_{i_2}) + \cdots \\
    &+ (-1^{n})\sum_{1\leq i_1 < i_2 < \cdots < i_{n-1} \leq n}P(D_{i_1}\land D_{i_2} \cdots \land D_{i_{n-1}}) + (-1^{n+1}) P(D_{1}\land D_{2} \cdots \land D_{n})
\end{align*}
$$

Enlightening I know. In essence, the idea is that if you subtract off the events happening two at a time to compensate for overcounting, you overcorrect the events with 3 or more coincidences. Iterating all the way down eventually achieves balance. If you like to think about probabilities as venn diagrams, consider 3 overlapping circles representig the events. The nice geometric interpretation is that to get the total area (i.e.) probability we add up the areas of the 3 circles but then have to correct by 
subtracting/adding parts where they intersect. 

Unfortunately it's not immediately obvious how to compute the probability that several of the events happen simultaneously. Under what conditions is a number divisible by several different primes? I can't do this one again, take it on good faith that this is true if and only if it's divisible by the product of the primes in question. Easy, then;

$$
\begin{equation*}
    P(D_{i_1}\land D_{i_2} \cdots \land D_{i_{k}}) = \frac{1}{p_{i_1}p_{i_2}\cdots p_{i_k}}
\end{equation*}
$$

Substiuting this back into expression for the total probability;

$$
\begin{align*}
    P(D_1\lor D_2 \lor ... \lor D_n) &= \sum_{1\leq i_1 \leq n}\frac{1}{p_{i_1}} - \sum_{1\leq i_1 < i_2 \leq n}\frac{1}{p_{i_1}p_{i_2}}+ \cdots \\
    &+ (-1^{n})\sum_{1\leq i_1 < i_2 < \cdots < i_{n-1} \leq n}\frac{1}{p_{i_1}p_{i_2}\cdots p_{i_{n-1}}} + (-1^{n+1}) \frac{1}{p_{1}p_{2}\cdots p_{n}}
\end{align*}
$$

and lastly, the probability we actually care about;

$$
\begin{align*}
    P(\neg D_1\land \neg D_2 \land ... \land \neg D_n) &= 1 - \sum_{1\leq i_1 \leq n}\frac{1}{p_{i_1}} + \sum_{1\leq i_1 < i_2 \leq n}\frac{1}{p_{i_1}p_{i_2}}+ \cdots \\
    &+ (-1^{n-1})\sum_{1\leq i_1 < i_2 < \cdots < i_{n-1} \leq n}\frac{1}{p_{i_1}p_{i_2}\cdots p_{i_{n-1}}} + (-1^{n}) \frac{1}{p_{1}p_{2}\cdots p_{n}}
\end{align*}
$$

This quantity is precisely equal to;

$$
\begin{equation*}
    \left(1 - \frac{1}{p_1}\right)\left(1 - \frac{1}{p_2}\right) \cdots \left(1 - \frac{1}{p_n}\right)
\end{equation*}
$$

Because the finite product of finitely many numbers is non zero, so too is the desired probability, (small as it might be).