---
title: "Euler's Theorem via Necklaces I"
date: 2024-05-15
permalink: /posts/2024/05/16/Eulers-Theorem-via-Necklaces-I/
tags:
  - Number Theory
  - Combinatorics
comments: false
layout: single
---

# Abstract
You may be aware of a cute proof of Fermat's Little Theorem that exploits rotational symmetries of necklaces. 
It's also possible you haven't heard of Fermat's Little Theorem (not to be confused with his last!), 
in which case I have the pleasure of acquainting you with both the theorem and the aforementioned proof. 
Fermat's Little Theorem (from now on FLT) can be seen as a special case of the more general 
Euler's Theorem (plus an edge case). One might ask if the combinatorial proof of FLT can be lifted to a proof of Euler's Theorem. 

In this post, I present in an elementary fashion the combinatorial roof of FLT and describe the relationship between the two theorems.
This is in anticipation of a second post in which I will present the lifted version of the proof of Euler's Theorem using slightly more technical machinery.

# Fermat's Little Theorem

**Fermat's Little Theorem**: If $$p$$ is a prime, then;

$$ p | a^p - a $$

for all integers $$a$$. 

The notation $$x | y$$ reads $$x$$ divides $$y$$ where $$x$$ and $$y$$ are understood 
to be integers. But what is a necklace, and how can we possibly hope to relate the two? Necklaces are combinatorial objects, but their exact definition
is not necessary to understand the basic scheme. The idea is simple, we will describe 
a collection of $$a^p - a$$ objects (necklaces) and then sort them into groups of size $$p$$. This is a very literal interpretation of the statement that 
$$a^p - a$$ is divisible by $$p$$. Now to construct our necklaces. To begin, we'll leave them unclasped, and pretend that a necklace is any old array of beads. Precisely, suppose we have $$a$$ 
different colours of beads in large (read, inexhaustible) bags. We construct a necklace by taking a number of beads and laying them out 
in some particular order. For example, if we have red ($$r$$) and blue ($$b$$) beads, one might look like;

$$brrbr$$

It has length $$5$$. How many such necklaces are there (red and blue of length $$5$$)? There are $$2$$ choices for each bead and so there are 
$$2^5$$ possible necklaces. In view of the theorem, we might cast $$a$$ as $$2$$ and $$p$$ as $$5$$ to recover $$a^p$$. We still need to 
lose $$a$$ ($$2$$) of them though. Is there a natural choice? Natural is arguable, but certainly the monochrome necklaces fit the bill as there 
are exactly $$a$$ of them, one for each colour. All in all, we are now considering 
the set of necklaces of length $$p$$ which are not monochrome, and there are exactly $$a^p - a$$ of these. Now to group them. 
We will assign two necklaces to the same group if they are actually the same necklace. That is, we thread our necklaces, close them, and say that 
two necklaces are really the same necklace if I can rotate one to make it look like the other. The group corresponding 
to our example;

$$
\begin{align*}
    &brrbr \\
    &rbrrb \\
    &brbrr \\
    &rbrbr \\
    &rrbrb
\end{align*}
$$

"Obviously" (bear with me) each necklace can be rotated $$p$$ times, in which case there are $$p$$ necklaces in each group and we're done! That we didn't 
need the fact that $$p$$ was prime should make you suspicious. Suppose $$p = 4$$. One possible necklace is $$rbrb$$. If we rotate it $$p$$ times;

$$
\begin{align*}
    &rbrb \\
    &brbr \\
    &rbrb \\
    &brbr 
\end{align*}
$$

we see that there are only 2 distinct necklaces in our group! The problem we've 
encountered is that it's possible to have cyclic patterns within our necklace. If a pattern of length $$d$$ 
(say, $$rbrb$$ with length $$2$$) tiles the necklace, then it belongs to a group of only $$d$$ necklaces. However, 
if a pattern of length $$d$$ tiles the necklace, then $$d$$ must divide $$p$$. Suddenly $$p$$ being prime comes to 
the rescue! Because $$p$$ is prime, if $$d | p$$, then either $$d = p$$, in which case the group has $$p$$ distinct necklaces as desired, or 
$$d = 1$$, which is to say that the pattern has only one bead and is therefore monochrome. Because we discarded all of 
the monochrome necklaces, we have only necklaces which belong to groups of size $$p$$, and this proves the theorem.


# Euler's Theorem
What do the numbers $$1,3,7$$ and $$9$$ have in common with $$10$$? Not much, in particular the only (positive) divisor each one shares 
with $$10$$ is $$1$$. We say that the former are the 'totatives' of $$10$$, the positive integers at most $$10$$ with which $$10$$ shares 
no common factors other than $$1$$. We define the Euler Phi function $$\varphi(n)$$ to be the number of totatives of $$n$$. 
Euler's Theorem is as follows 


**Euler's Theorem**: If $$a$$ is coprime with $$n$$, then

$$
\begin{equation*}
    n | a^{\varphi(n)} - 1.
\end{equation*}
$$

There's a passing resemblance but it's not obvious that this is a generalisation of FLT. If it were, then we would expect to be able to take 
$$p = n$$ and recover the statement of the theorem. $$-1$$ in place of $$-a$$ is not promising, but for the time being we should try to understand 
$$\varphi(p)$$. Which of the numbers less than $$p$$ are its totatives? Almost by definition, all of them. Suppose $$n < p$$, and $$d$$ is a common 
factor of them both. Because $$d|p$$ and $$p$$ is prime, $$d$$ can only be $$1$$ or $$p$$. Because $$d | n$$, $$d \leq n < p$$, and therefore cannot be the 
latter. It follows that $$d$$ is $$1$$. Therefore, every number less than $$p$$ is a totative, and $$\varphi(p) = p-1$$. Now the theorem reads;

$$
\begin{equation*}
    p | a^{p-1} - 1
\end{equation*}
$$

But then $$p$$ certainly divides a multiple of $$a^{p-1} - 1$$, in particular $$a(a^{p-1} -1) = a^p - a$$ and we deduce FLT.. Not quite, 
we did assume that $$a$$ is coprime with $$p$$ whereas the statement of FLT was unconditional. If this is not the case, and they share a common factor larger than $$1$$, then it must be $$p$$, 
for similar reasons to those outlined previously. But if $$a$$ is divisible by $$p$$, then certainly $$a^p - a = a(a^{p-1} - 1)$$ is, and so with 
only a minor detail we recover FLT from Euler's Theorem. It is in this sense that I suggest the latter generalises the former. 