---
title: "Demystifying Euler's number"
date: 2025-01-11
permalink: /posts/eulers_number/
tags:
  - tutorial
  - mathematics
---

_THIS POST IS CURRENTLY UNDER CONSTRUCTION_

_Euler's number $e := 2.71828\dots$ has, to me, always been a semi-mysterious number. While I understood many facts about $e$, I never felt I ever truly understood what it really was -- it's core essence so to speak. Thanks to an excellent explanation by [Grant Sanderson](Grant Sanderson)'s [3Blue1Brown video](https://www.youtube.com/watch?v=m2MIpDrF7Es), I now better understand this constant.  In this blog post, I will attempt to describe, in my own words, my understanding of Euler's number and expound on Sanderson's explanation._

Introduction
------------

Euler's number $e := 2.71828\dots$ has, to me, always been a semi-mysterious number. While I understood many facts about $e$, I never felt I ever truly understood what it really was -- it's core essence so to speak. Sadly, it was only very recently that I finally felt like I truly understood this constant. Sure, I knew certain _facts_ about $e$, but I didn't really understand its _essence_. For example, I knew that,

$$\frac{de^x}{dx} = e^x$$

I also knew that $e$ was used in calculations involving compound interest due to the fact that

$$e = \lim_{n \rightarrow \infty} \left(1 + \frac{1}{n}\right)^n$$

but these facts were not satisfactory to me because they didn't explain exactly why this constant is so ubiqituous. Why, for example, do we choose to represent nearly every logarithm with base $e$? More puzzingly, why do we call this the "natural" logarithm? Why does it appear in the probability density function for the [normal distribution](https://en.wikipedia.org/wiki/Normal_distribution)? Or in [Euler's formula](https://en.wikipedia.org/wiki/Euler%27s_formula)? 

With the help of [Grant Sanderson](Grant Sanderson)'s excellent [3Blue1Brown video](https://www.youtube.com/watch?v=m2MIpDrF7Es), I feel now that I have a much better understanding for it's essence. In this blog post, I will attempt to describe, in my own words, my understanding of Euler's number and expound on Sanderson's explanation.

To spoil the punchline, Euler's constant is, in a sense, a number that describes all exponential functions -- that is, functions of the form $f(x) := a^x$. Because of this, all exponential functions of the form $a^x$ can be written in a "canonical" way using $e$ that is more arguably more informative than $a^x$. Let's dig in.

The essence of exponential functions
------------------------------------

To review, exponential functions are functions of the form:

$$f(x) := a^x$$

for some constant $a$. Exponential functions do not only grow, but their _growth_ also grows. When plotted, they look like the following:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/exponential.png" alt="drawing" width="400"/></center>

In fact, the key characteristic of exponential functions -- the very characteristic _defines_ exponential functions -- is that their growth grows linearly with the function itself. Stated more rigorously, **an exponential's derivative _is proportional_ to the value of the function itself.** That is:

$$\frac{da^x}{dx} = Ka^x$$

where $K$ is some constant that is determined by $a$. 

That is, no matter what value for $x$ for which we are evaluating the derivative, the derivative of $a^x$ is simply $a^x$ itself multiplied by some constant $K$. Intuitively, this makes sense just by looking at the exponential function curve: the bigger is $a^x$ the steeper the rate of change:

 <center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/exponential_proportional_to_value.png" alt="drawing" width="400"/></center>

This fact can be proven mathematically. Let's start with the definition of the derivative of $a^x$:

$$\begin{align*}\frac{da^x}{dx} &= \lim_{h \rightarrow 0} \frac{a^{x+h} - a^x}{h} \\ &= \lim_{h \rightarrow 0} \frac{a^xa^h - a^x}{h} \\ &= a^x \underbrace{\lim_{h \rightarrow 0} \frac{a^h - 1}{h}}_{K} \end{align*}$$

Note, that the derivative of $a^x$ is simply $a^x$ scaled by a constant:

$$K := \lim_{h \rightarrow 0} \frac{a^{h} - 1}{h}$$

Moreover, we see that this constant is determined by the value of $a$ -- that is, it is a function of $a$. Thus, we can write this constant as:

$$k(a) := \lim_{h \rightarrow 0} \frac{a^{h} - 1}{h}$$ 

Defining Euler's number
-----------------------

Now, the natural question that follows from this observation of exponential functions is: what exponential function, $a^x$, yields a constant of 1? That is, for what value of $a$ do we have $k(a) = 1$?. It's Euler's number! 

That is, Euler's number is the base of the exponential function for which the derivative of that exponential function is the exponential function itself:

$$\frac{de^x}{dx} = e^x$$

That is, $e$ is the value for $a$ that satisfies the following equation:

$$1 = k(a) = \lim_{h \rightarrow 0} \frac{a^{h} - 1}{h}$$

It turns out that that $e$ can be expressed as a limit that enables us to compute numerical approximation to this value (See Theorem 1 in the Appendix to this post):

$$e = \lim_{n \rightarrow \infty} \left(1 + \frac{1}{n}\right)^n$$

With this formula, we can calculate ever close approximations to $e$ by simply plugging in larger and larger values for $n$. If we do so, we find that $e \approx 2.71828$.

In a sense, $e$ defines the "base" exponential function; By "base" I mean the exponential function whose rate of change is itself (i.e., whose constant of proportionality is 1).

All exponential functions can be expressed in a more intuitive way with $e$
---------------------------------------------------------------------------

The next natural question is, why do we care about $e$? And why do we see so many exponential functions and logarithms involving $e$?

To answer this, let's first say we have some exponential function $a^x$. As we showed above, the derivative of $a^x$ is proportional to $a^x$ with some constant of proportionality given by $k(a)$. Knowing this constant of proportionality would be quite informative: it tells us exactly how quickly the exponential is growing. 

Unfortunately, the specific value, $k(a)$, is not easy to compute directly from $a$. Recall it is given by,

$$k(a) := \lim_{h \rightarrow 0} \frac{a^{h} - 1}{h}$$ 

Is there some way to express $a^x$ in a way that involves $k(a)$? Yes! And that is given by:

$$a^x = k(a) e^x$$

See Theorem 2 in the Appendix to this post.

Because every value for $a$ is associated with a unique constant $k(a)$, we can express all exponential functions using the constant $k(a)$ instead of $a$ via $k(a) e^x$. This value makes the exponential easier to interpret: whenever you come upon an exponential function, $f(x) := K e^x$, the rate of change of $f(x)$ at $x$ is given by $K$.

Connection to compound interest
-------------------------------

Euler's number was actually discovered first by [Jacob Bernoulli](https://en.wikipedia.org/wiki/Jacob_Bernoulli) as it relates to [compound interest](https://en.wikipedia.org/wiki/Compound_interest). In fact, $e$ is often introduced to students in this way and it's only discussed in relation to exponential functions in more advanced math courses. Let us now approach $e$ from the perspective of compound interest and connect it from this perspective back to exponential functions.

Say we have one dollar and we lend that dollar out at an interest rate $r$ over some unit of time (e.g., one year). After that time passes, that $1 earns an additional $r$ -- if $r$ is 1 (i.e., 100% interest), then we would end up with a total amount of money of $2:

$$\begin{align*}\text{Total} &:=  1 + r \\ &= 1 + 1 \\ &= 2\end{align*}$$

However, because the interest wasn't paid out until the end of the perscribed unit of time, the interest itself was not given the opportunity to earn money. Let's now say that interest is paid out every half unit of time (e.g., every six months instead of every year). Then after 6 months, if our interest rate is 100%, the $1 earns $0.50. That $0.50 can now be lent out for the remaining six months and earn an additional $0.25 (at 100% interest, but half the unit of time). The total interest earned would now be $1.25 ($1 from the original $1 and $0.25 from the $0.50):

$$\begin{align*}\text{Total} &:=  \underset{\text{Value after second payment}} { \underset{\text{Value after first payment}{\left(1 + \frac{1}{r} \right)} } \left(1 + \frac{r}{2} \right) } \end{align*}

That is, in the first payment, we would have $(1 + \frac{r}{2})$


We can play this game again and now instead of compounding twice, it compounds three times (once every four months). Now, after 4 months, the $1 would earn $0.33. That $0.33 has the opportunity to earn for the rest of the year and so on and so forth. 

Stated mathematically, if we start with $1, we have an interest rate $r$, and we compound once, the total money at the end would simply be:

$$\text{Total} :=  1 + r$$

If we compound twice, we would end up with:

$$\text{Total} :=  (1 + \frac{r}{2})^2$$

If we compound three times, we would end up with:

$$\text{Total} :=  (1 + \frac{r}{n})^n$$

If we compound an infinite number of times (i.e., every possible instant of time), the total we would end up with would be given by:

$$\text{Total} :=  \lim_{n \rightarrow \infty} (1 + \frac{r}{n})^n$$

If the interest rate is 100% (which is 1 as a ratio to the value lent), then the total we end up with is  

$$\text{Total} :=  \lim_{n \rightarrow \infty} (1 + \frac{1}{n})^n$$

This is $e$! 

In the context of our discussion regarding the derivative of exponential functions, this makes intuitive sense. 





Appendix
--------

<span style="color:#0060C6">**Theorem 1 (Value of $e$):** The value for $e$ is given by the following limit:</span>

<center><span style="color:#0060C6">$$e = \lim_{n \rightarrow \infty} \left(1 + \frac{1}{n}\right)^n$$</span></center>

**Proof:**

Let

$$f(x) := e^{x}$$

and

$$f'(x) = \frac{df(x)}{dx}$$

We know the following facts about $f(x)$: 

$$\begin{align*}$f(0) &= e^0 = 1 \\ f'(x) &= f(x) \end{align*}$$

Note that $f'(x) = f(x)$ is a first-order differential equation and $f(0) = 1$ is an initial condition. Thus, given an arbitrary value for $x$, we can solve for $f(x)$ by solving this [initial value problem](https://en.wikipedia.org/wiki/Initial_value_problem#:~:text=In%20multivariable%20calculus%2C%20an%20initial,given%20point%20in%20the%20domain.). We can do so using the [Euler Method](https://en.wikipedia.org/wiki/Euler_method).

In order to solve for $f(x)$, we will use Euler's method with increments of $\Delta t := x/n$ for some number of increments $n$. 

We first note that for an arbitrary value of $t$, we can approximate $f(t + \Delta t)$ via

$$f(t + \Delta t) \approx f(t) + \Delta t f'(t) $$

Because $f'(t) = f(t)$, we have

$$\begin{align*}f(t + \Delta t) &\approx f(t) + \Delta t f'(t)  \\ &= f(t) + \Delta t f(t) \\ &= f(t)(1 + \Delta t) \end{align*}$$

Using this formula, we can solve for $f(x)$ by starting at $t := 0$ and stepping towards $f(x)$ at increments of $\Delta t := \frac{x}{n}$ using the equation above. For the first step, where $t := 0$, we have

$$\begin{align*}f(0 + \Delta t) &\approx f(0) (1 + \Delta t) \\  &= 1 + \frac{x}{n}\end{align*}$$

Taking the second step, we have

$$\begin{align*} f\left(\frac{x}{n} + \Delta t\right) &\approx f\left(\frac{x}{n} \right) (1 + \delta t) \\  &= \left(1 + \frac{x}{n}\right) \left(1 + \frac{x}{n}\right) \\ &= \left(1 + \frac{x}{n}\right)^2 \end{align*}$$

Extrapolating this all the way to $n$ steps, arriving at $f(x)$, we see that

$$\begin{align*}f(x) &= f\left( n\frac{x}{n} \right) \\ &= f\left( (n-1)\frac{x}{n} + \frac{x}{n} \right) \\ &=  \left( 1 + \frac{x}{n} \right)^{n-1} \left( 1 + \frac{x}{n} \right) \\ &=  \left( 1 + \frac{x}{n} \right)^{n}  \end{align*}$$

Finally, to derive $e$ itself, we plug in $x = 1$ and see that

$$f(1) = e^1 = e \approx \left( 1 + \frac{1}{n} \right)^{n}$$

Note that, as $n \rightarrow \infty$, this formula will converge on the true value of $e$ and thus,

$$e = \lim_{n \rightarrow \infty} \left( 1 + \frac{1}{n} \right)^{n}$$

$\square$



