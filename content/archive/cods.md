---
title: "Approximation of the limit of Divergent Series"
date: 2018-08-25T16:20:21-05:00
---

"Divergent series are an invention of the devil and it is shameful to
base on them any demonstration whatsoever." - @Abel -- N.H. Abel. 1826

Mathematics is the science of skilful operations, which are dealing with the
logic of shape, quantity and rearrangement. Mathematics is using its core
principles and rules to solve problems and get a reasonable answer. In my
opinion, mathematics will soon run out of interesting theories if all new
theories will formulate in terms of invented concept, which appear in
axioms. This exploration is about finding finite values, limits for famous
divergent series and later analytically extending Euler-Riemann's zeta function
to find a limit for any divergent series that can be formed by Euler- Riemann's
zeta function.

Introduction
============

I tend to think that in order to create innovative theories, mathematics
as a whole should be pushed to its boundaries and limits, new axioms
should be invented and unexplored topics should be studied. With this
kind of approach, I got acquainted with the divergent series. It all has
started in my former school when I was in 7 th grade and we have started
the topic of geometric series. When my teacher asked a question --
"What will be the infinite sum of one, a half, a quarter and so on?"
Initially, I thought the answer was infinity, because at that time it
made sense to me, an infinite amount of values equals to always growing
sum until it reaches infinity. When the teacher told us the answer is
two, I was quite shocked by the fact that it has an end and all these
values are converging to one finite value. I remember how I was walking
around and trying to understand, why this series does not go beyond that
finite value? It was logical to me that if it keeps summing every
element, every element should contribute to the goal of getting closer
to that value and there should be one element, which after summing up
will go beyond two. I started reading and researching additional
material to understand the fundamental logic of convergent series. When
I finally understood why it works, I found a new topic, that struck my
mind -- "Divergent series" and not the series in general, but how the
most famous mathematicians: Leonhard Euler, Bernhard Riemann and
Srinivasa Ramanujan proved that these series are in nature convergent
too. Now it all made a perfect sense.

In this exploration I will explore the most famous and well-known
divergent series, proving with multiple ways that they have a finite
value that they are converging too and at the end, I will show how it is
possible to find limit almost for any divergent series.

Grandi's Series
================

This is probably one of the famous and trickiest-at-the-beginning
divergent series. It looks like this:

```
1-1+1-1+1-1+...=\sum_{n=1}^{\infty} (-1)^{n-1}
```

Strange, isn\'t? For the first time, it has been reported by
mathematician Guido Grandi in 1703. He noticed that inserting
parenthesis into the series will return a different result, but these
parentheses are being inserted in a way, that it should not affect the
series value. Let me show you:

```
Parenthesis before even elements: 1-(1-1)-(1-1)-(1-1)...=1
Parenthesis before odd elements: (1-1)+(1-1)+(1-1)+(1...=0
```

Grandi explained this phenomenon by saying that -- \"Mettendo in modo
diverso le parentesi nell\'espressione $1-1+1-1+...$ io posso,
volendo, ottenere 0 o 1. Ma allora l\'idea della creazione ex nihilo è
perfettamente plausibile.\"@Mettendo Which translates from Italian to
English - \"By putting parentheses into the expression $1-1+1-1+...$
in different ways, I can, if I want, obtain 0 or 1. But then the idea of
the creation ex nihilo is perfectly plausible.\" Where \"ex nihilo\"
means \"out of nothing\".@Exnihilo As a true mathematician, Leonhard
Euler did not think that the value is either 0 or 1, he thought that the
true limit was $1/2$. He proved it through the geometric reasoning of
the \"Witch of Agnesi\". We will prove it arithmetically.

First Solution
--------------

This is pretty easy and convenient solution for rearranging and
ordering. Let us denote Grandi's series by *S*, so `S=1-1+1-1+...`.
Further, we will subtract *S* from 1, and then we will get:

```
  1-S&=1-(1+1-1+1-1+...)
  1-S&=1-1+1-1+1-...
  1-S&=S
  2S&=1
  S&=1/2
```

Second Solution
---------------

We can formulate the second solution by using the infinite formula for
converging geometric series - $\frac{a}{1-r}$, where $a$ is the first
element of the series and $r$ is the common ratio. Generally, the
formula is applicable only of absolute value of the common ration is
less than one, $|r| < 1$ but it is also applicable in our case, where
$r = - 1$. In this case, let us denote Grandi\'s series as *S*, and

\begin{equation*}
S=\frac{1}{1-(-1)}=\frac{1}{1+1}=\frac{1}{2}
\end{equation*}

This proves how the series converges to $1/2$. This is the solution that
I thought about, when I imagined the Grandi\'s series as a geometric
series.

Third Solution
--------------

Third solution can by achieved by using partial sums. So that the
series\'s sum will be:

```
  1   -1   +1   -1   +1   -1   +1   $...$
  --- ---- ---- ---- ---- ---- ---- ----------
  1   0    1    0    1    0    1    $...$
```

By averaging the sums, we can conclude that:

```
  1   $(1+0)/2$   $(1+0+1)/3$   $(1+0+1+0)/4$   $(1+0+1+0+1)/5$
  --- ----------- ------------- --------------- -----------------
  1   $1/2$       $2/3$         $1/4$           $3/5$
```

Therefore, we can evaluate that with each even indexes the series equal
to $1/2$ and with odd indexes, the partial sums converge to $1/2+1/2n$,
where *n* is the amount of elements summed up. If the amount of indexes
tends to infinity then $1/2n$ will be infinitely small, resulting that
the infinite partial sums will converge to $1/2$.

Wolff\'s series (1-2+3-4+5-6+...)
======================================

This series is quite fascinating too. When Guido Grandi has published
his work on his infinite series that we explored above, famous
mathematician Christian Wolff doubted the logic of Grandi\'s series and
because of that, he wrote a letter to Gottfield Wilhelm Leibniz. After
receiving a reply @Wolff from Leibniz, Wolff was so pleased with the
solution that he wanted to extend the series to $1-2+3-4+5-6+...$


### Click here to open the full paper [cods.pdf](../cods.pdf)