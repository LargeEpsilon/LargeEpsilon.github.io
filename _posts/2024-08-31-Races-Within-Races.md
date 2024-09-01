---
title: "Races Within Races"
date: 2024-08-31
permalink: /posts/2024/08/31/Races-Within-Races/
tags:
  - The Pigeon Hole Principle
comments: true
layout: single
---

# Abstract
Somewhat recently a number of my friends participated in Sydney's City2Surf, a 14km run from the CBD to Bondi. These friends also regularly participate in 'Park Runs' most Saturday mornings, 
5km runs held in parks throughout the city. Ben is one of these friends. Ben takes his running quite seriously. Amazingly, his City2Surf performance was so stellar that he actually set a new 5km record! 
In fact, his total 14km pace almost rivalled his previous personal best 5km pace. This prompted the following question, if one runs a long race at a certain pace, is it necessarily the case that for any 
given shorter race, the long race contains a complete short race within it at the same pace or better? Amongst all races, what is the slowest fastest short race contained in a long race? How much wood 
would a wood chucker chuck if a wood chucker could chuck wood? Join me on a mathematically low tech journey to ask and answer two of these inane questions.

## Formalising the question
Let's put aside the general question for a moment and study Ben's achievement. If his 14km pace was in fact better than his previous best 5km pace, was it a given that his 14km run contained within it a 5km segment of this pace or better? 
It turns out this is moderately difficult to answer, but at least we have an idea of the sort of question we would now like to ask. Regarding the second of my tongue twisters, I'm really just pushing the previous question 
a little further. Maybe it does contain a pb 5km segment, maybe it doesn't, but we will know for certain if we can answer the following more difficult question; 
Ben runs a 14km run at a certain pace (say 4 minute k's to be concrete), what is the best 5km pace his 14km run is guaranteed to contain, no matter how he speeds up or slows down during the race? This is what I was alluding 
to by the 'fastest slowest race' (for the annoying math literates amongst my readers I am of course referring to a supremum over an infimum). To generalise just take variables for each of the values in the above.

## A simple case
As is often the case, it is easiest to turn to a simple case which hopefully will shed light on some of the difficulties of the general problem. What simplifcations can be made? There is something discordant about the values playing the part of the short and long races, namely 5 does not divide 14. There is a very natural impulse to chop up the long race into a discrete number of the short races, but this is not possible. Let's bump the long race up to 15km to give ourselves that freedom and see 
where it leads us. Ok, I run a 15km race (fat chance) in 3 5km segments, what can I say about my pace in each of these legs. The key insight is this, my pace in each 5km segment can't be 'below average'. If I ran the 15km at pace $$v$$, and my 
pace in each of the 3 5km legs was less than $$v$$, then my average pace would be less than $$v$$. It follows that at least one of 5km segments was ran at an average or above pace. So we've answered our first question, and we have a lower bound on what the best pace must be, but we would like a precise answer rather than an inequality to answer our second question. To those with some familiarity with stupid mathematical puzzles the next step is obvious. What we really want to do is introduce an upper bound on what the best pace can be. Ideally, our upper bound will match our lower bound. If I tell you that $$x \leq y \leq x$$ it follows that $$y = x$$, although this is a funny seeming way to establish the fact. How to establish this upper bound? 
In some way this is the easy part, all I have to do is produce one way to run 15km such that the best 5km run contained within it has pace equal to the average pace. By way of our previous argument, we can see that any slow segment must be balanced by a fast segment to preserve the average, so we just homogenise the race. Coast by the whole race at the same pace and you don't have to be too concerned about what your best 5km pace is. Great! In any 15km race of a given pace, the best 5km pace guaranteed to exist within it is equal to the average pace of the race. I hope it is obvious that we can replace the numbers 5 and 15 with any two numbers such that the latter is a multiple of the former.

## The general case
Why doesn't the previous approach work in general? Well, I can't necessarily segment the long race into discrete multiples of the short race without remainder. I think a big part of the reason this problem was difficult (at least for me) was that 
after seeing the relatively clean solution to the special case, it was difficult to shake my intuition that the same result (if not the same argument) should be applicable in general. Alas this is not true. Here's the best lower bound we can get using 
a similar method. Let $$L$$ be the length of the long race, and $$S$$ the length of the short race. Write $$L = qS + r$$ in the usual quotient remainder way, i.e. $$q$$ is a positive integer and $$0 < r < S$$. Then we have segmented the race into $$q$$ short legs with a leftover $$r$$ sprint to the finish. Here's one observation. The $$kq$$ short legs can't have taken longer to complete than the whole race, it follows that there is some minimum average pace for the $$q$$ legs below which they would have taken too long to complete. By the argument used in the special case, at least one of the legs must have been run at this pace or better. Lets try to make this argument quantitative. 

Let $$v$$ be the pace of the race. Then the time taken for the race is completely determined, $$ T = L/v $$. If the average pace of the short segments is greater than $$qS/T$$ (i.e. what we would get if we were to divide the total time between the various segments), then the total time taken for the race would exceed $$T$$. It follows that the average pace is less than or equal to $$qS/T$$, and one of the segments is run at this pace or better. How does this compare to $$v$$? Well, what we've really done is put an $$L$$km time on a $$qS$$km distance, one can easily verify tht $$qS/T = v\left(\frac{qS}{L}\right)$$. It is unclear to how to turn this to an upper bound. If we try to literally implement it by running the first $$q$$ segments at this pace and teleport the last $$r$$km then the final $$S$$ km include the breakneck speed as well as the homogenous pace, and therefore its average pace would exceed the lower bound. What we really need is to homogenise *all* $$qkm$$ intervals. Here is a construction I found. Chop up the race into alternating segments of length $$r$$ and $$S-r$$, starting and ending with the former. Importantly, everu $$S$$km segment now contains (in aggregate) exactly one full $$S-r$$km segment and one $$r$$km segment. Suppose I have a fast pace $$v_r$$ and a resting pace $$v_{S-r}$$ and I run the race alternating between these two paces. This pacing isn't so ridiculous, when I run it does look something like this in many cases (be kind). These two paces are related by my average pace $$v$$ in the following way;

$$
\begin{equation*}
    (q+1)\frac{r}{v_r} + q\frac{S-r}{v_{S-r}} = \frac{L}{v}
\end{equation*}
$$

This is simply an expression of the fact that the time taken by all the various segments must add up to the whole. For no particular reason let me present the equality in the following way

$$
\begin{equation*}
    \frac{r}{v_r} + \frac{S-r}{v_{S-r}} = \frac{1}{q}\left(\frac{L}{v} - \frac{r}{v_r}\right)
\end{equation*}
$$

Now, we know that each $$S$$km segment will have the same pace because each contains $$r$$km run at $$v_r$$ and $$S-r$$km run at $$v_{S-r}$$, what is this pace? 

$$
\begin{align*}
    \frac{S}{\frac{r}{v_r} + \frac{S-r}{v_{S-r}}} &= \frac{qS}{\frac{L}{v} - \frac{r}{v_r}}
\end{align*}
$$

Great, we understand how the average pace depends now on  $$v_r$$. Because we are trying to understand an upper bound, we would like this quantity to be as low as possible. The smaller $$r/v_r$$ is, the lower this will be. Therefore, taking the limit of $$v_r$$ to infinity we find that the optimal lower bound is;

$$
\begin{equation*}
    \frac{qS}{\frac{L}{v}} = v\left(\frac{qS}{L}\right)
\end{equation*}
$$

as desired. 

## Ben's Run/An open Question?
Applying the conclusion above we can see that no matter how Ben ran his City2Surf, he was guaranteed a 5km pace at least 10/14 as good as his total pace. His 14km time was good but not that good, so he must have kept a pretty consistent pace, kudos Ben. An unsatisfying element of this solution is that to attain the other bound we would require infinitely fast segments, i.e. teleporting! Is it possible to find a construction guaranteeing the upper bound with only finite speeds? My gut says no, but I have no proof.