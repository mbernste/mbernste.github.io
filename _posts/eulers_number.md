---
title: "Demystifying Euler's number"
date: 2023-10-17
permalink: /posts/eulers_number/
tags:
  - tutorial
  - mathematics
---

_THIS POST IS CURRENTLY UNDER CONSTRUCTION_

_For me, Euler's number $e := 2.71828\dots$ was a somewhat mysterious number that I sort of took for granted. Thanks to an excellent explanation by [Grant Sanderson](Grant Sanderson)'s [3Blue1Brown video](https://www.youtube.com/watch?v=m2MIpDrF7Es), I now better understand this constant.  In this blog post, I will attempt to describe, in my own words, my understanding of Euler's number and expound on Sanderson's explanation._

Introduction
------------

For me, Euler's number $e = 2.71828\dots$ was a somewhat mysterious number that I sort of took for granted. Sadly, it was only very recently that I finally felt like I truly understood this constant. Sure, I knew some _facts_ about $e$, but I didn't really understand its _essence_. For example, I knew that,

$$\frac{de^x}{dx} = e^x$$

I also knew that $e$ was used in calculations involving compound interest due to the fact that

$$e = \lim_{n \rightarrow \infty} \left(1 + \frac{1}{n}\right)^n$$

but these facts were not satisfactory to me because they didn't explain exactly why this constant is so ubiqituous. Why, for example, do we choose to represent nearly every logarithm with base $e$? More puzzingly, why do we call this the "natural" logarithm? Why does it appear in the probability density function for the [normal distribution](https://en.wikipedia.org/wiki/Normal_distribution)? Or in [Euler's formula](https://en.wikipedia.org/wiki/Euler%27s_formula)? 

With the help of [Grant Sanderson](Grant Sanderson)'s excellent [3Blue1Brown video](https://www.youtube.com/watch?v=m2MIpDrF7Es), I feel now that I have a much better understanding for it's essence. In this blog post, I will attempt to describe, in my own words, my understanding of Euler's number and expound on Sanderson's explanation.

To spoil the punchline, Euler's constant is, in a sense, a number that describes all exponential functions -- that is, functions of the form $f(x) := a^x$. Because of this, all exponential functions of the form $a^x$ can be written in a "canonical" way using $e$ that is more arguably more informative and "natural" (hence "natural" logarithm) than $a^x$. Let's dig in.

The essence of exponentials
---------------------------

To review, exponential functions are functions of the form:

$$f(x) := a^x$$

for some constant $a$. Exponential functions do not only grow, but their _growth_ also grows. When plotted, they look like the following:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/exponential.png" alt="drawing" width="400"/></center>

The _key characteristic_ of exponential functions that, in a sense defines exponential functions, is that their derivatives _are proportional_ to the functions themselves. That is:

$$\frac{da^x}{dx} = Ka^x$$

for some particular constant $K$ that is determined by $a$. That is, no matter what value for $x$ for which we are evaluating the derivative, the derivative of $a^x$ is simply $a^x$ itself multiplied by some constant $K$. Intuitively, this makes sense intuitively just by looking at the exponential function curve: the bigger is $a^x$ the steeper the rate of change:

 <center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/exponential_proportional_to_value.png" alt="drawing" width="400"/></center>

To see this more rigorously, let's start with the definition of the derivative of $a^x$:

$$\begin{align*}\frac{da^x}{dx} &= \lim_{h \rightarrow 0} \frac{a^{x+h} - a^x}{h} \\ &= \lim_{h \rightarrow 0} \frac{a^xa^h - a^x}{h} \\ &= a^x \underbrace{\lim_{h \rightarrow 0} \frac{a^h - 1}{h}}_{K} \end{align*}$$

Note, that the derivative of $a^x$ is simply $a^x$ scaled by a constant:

$$K := \lim_{h \rightarrow 0} \frac{a^{h} - 1}{h}$$

Moreover, we see that this constant is determined by the value of $a$ (i.e., it is a function of $a$). In a sesne, this is the key defining feature of exponential functions. It differentiates exponential functions from other types of functions: the rate of change of the exponential function is simply the value of that function multiplied by a constant.

Defining Euler's number
-----------------------

Now, the natural question that follows from this observation of exponential functions is: what exponential function, $a^x$, yields a constant of 1? That is, what value of $a$ leads to $K = 1$? It's Euler's number! 

That is, Euler's number is simply defined to be the base of the exponential function for which the derivative of that exponential function is the exponential function itself:

$$\frac{da^x}{dx} = a^x$$

That is, $e$ is the value for $a$ that satisfies the following equation:

$$1 = \lim_{h \rightarrow 0} \frac{a^{h} - 1}{h}$$

Said another way, $e$ is the base of the exponential function whose rate of change changes in unison with the value of the function itself.

It turns out that that $e$ can be expressed as a limit that enables us to compute numerical approximation to this value:

$$e = \lim_{n \rightarrow \infty} \left(1 + \frac{1}{n}\right)^n$$

See Proof 1 in the Appendix to this post proving that this limit satisfies the aforementioned equation. Note that we can calculate ever close approxiamtions to $e$ by simply plugging in larger and larger values for $n$ in to the formula above. We find that $e \approx 2.71828$.

We see that $e$, in a sense, defines the "base" exponential function -- by "base" I mean the exponential function whose rate of change is itself (i.e., whose multiplying constant is 1).

All exponential functions can be expressed in a more intuitive way with $e$
---------------------------------------------------------------------------

The next natural question is, why do we care about $e$? What makes $e$ helpful? And why do we see so many exponential functions and logarithms involving $e$?

First, let's say we have some exponential function $a^x$. As we showed above, the derivative of $a^x$ is proportional to $a^x$ with some constant of proportionality $K$. However, given the value for $a$, we don't actually know $K$ (one would need to calculate it). Is there some way to express $a^x$ that involves the term $K$? Yes! And that is given by:

$$a^x = Ke^x$$

Because every value for $a$ is associated with a unique constant $K$, we can express all exponential functions as $K e^x$ instead of $a^x$. Because this new form involves $K$, one can argue that it is much more informative than $a^x$; It describes the exponential function whose rate of change is equal to $K$ times the value of that exponential function!

Appendix
--------

