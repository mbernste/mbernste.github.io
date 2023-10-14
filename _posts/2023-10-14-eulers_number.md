---
title: "Demystifying Euler's number"
date: 2022-10-14
permalink: /posts/eulers_number/
tags:
  - tutorial
  - mathematics
---

_THIS POST IS CURRENTLY UNDER CONSTRUCTION_

_For me, Euler's number $e := 2.71828\dots$ was a somewhat mysterious number I just sort of took for granted. Thanks to an excellent explanation by [Grant Sanderson](Grant Sanderson)'s [3Blue1Brown video](https://www.youtube.com/watch?v=m2MIpDrF7Es), I now better understand this constant.  In this blog post, I will attempt to describe, in my own words, my understanding of Euler's number and expound on Sanderson's explanation._

Introduction
------------

For many people I've talked to, Euler's number $e := 2.71828$ is a somewhat mysterious number one is sort of forced to just take for granted. Sadly, it was only very recently that I finally felt like I truly understood this constant. Sure, I knew some _facts_ about $e$, but I didn't really understand its _essence_. For example, I knew that 

$$\frac{de^x}{dx} = 1$$

but did not know why this constant is so ubiqituous. Why, for example, do we choose to represent nearly every logarithm with base $e$? More puzzingly, why do we call this the "natural" logarithm? Why does it appear in the probability density function for the [normal distribution](https://en.wikipedia.org/wiki/Normal_distribution)? Or in [Euler's formula](https://en.wikipedia.org/wiki/Euler%27s_formula)? 

With the help of [Grant Sanderson](Grant Sanderson)'s excellent [3Blue1Brown video](https://www.youtube.com/watch?v=m2MIpDrF7Es), I feel now that I have a much better understanding for it's essence. In this blog post, I will attempt to describe, in my own words, my understanding of Euler's number and expound on Sanderson's explanation.

To spoil the punchline, Euler's constant is used to express exponential functions -- functions of the form $f(x) := a^x$ -- in a "canonical" way. That is, every function $a^x$ can be expressed as $e^{Kx}$ for some constant $K$. As we will describe, there is good reason to prefer this "canonical" form! Let's dig in.

The essence of exponentials
---------------------------

To review, exponential functions are functions of the form:

$$f(x) := a^x$$

for some constant $a$. Exponential functions do not only grow, but their _growth_ also grows. They look like the following:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/exponential.png" alt="drawing" width="400"/></center>

A crucial characteristic of exponentials is that the derivative of an exponential function _is proportional_ to the function itself. That is:

$$\frac{da^x}{dx} = Ka^x$$

for some particular constant $K$ that is determined by $a$. Intuitively, this makes sense just based on looking at the exponential function curve: the bigger we see $a^x$ the steeper the rate of change:

 <center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/exponential_proportional_to_value.png" alt="drawing" width="400"/></center>

To see why this is true more rigorously, let's start with the definition of the derivative of $a^x$:

$$\begin{align*}\frac{da^x}{dx} &= \lim_{h \rightarrow 0} \frac{a^{x+h} - a^x}{h} \\ &= \lim_{h \rightarrow 0} \frac{a^xa^h - a^x}{h} \\ &= a^x \underbrace{\lim_{h \rightarrow 0} \frac{a^h - 1}{h}}_{K} \end{align*}$$

Note, that the derivative of $a^x$ is simply $a^x$ scaled by some constant,

$$K := \lim_{h \rightarrow 0} \frac{a^{h} - 1}{h}$$

Moreover, we see that this constant is determined by the value of $a$ (i.e., it is a function of $a$). In some sense, this is what differentiates exponential functions from other types of functions: the rate of change of the exponential function is simply the value of that function multiplied by some constant.


Defining Euler's number
-----------------------

Now, the natural question that follows from this observation is: what exponential function, $a^x$, yields a constant of 1? That is, what value of $a$ leads to $K = 1$? It's Euler's number! 

That is, Euler's number is simply defined to be the base of an exponential function for which the derivative of that exponential function is the exponential function itself. To derive Euler's number, you can simply solve for $a$ in the following equation:

$$1 = \lim_{h \rightarrow 0} \frac{a^{h} - 1}{h}$$


Expressing exponential functions in a canonical way
---------------------------------------------------







