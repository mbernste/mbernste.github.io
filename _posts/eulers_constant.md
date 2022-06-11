_For many people I've talked to, Euler's constant $e := 2.71828$ is a somewhat mysterious number one sort of just forced to take for granted. Thanks to an excellent explanation by [Grant Sanderson](Grant Sanderson)'s [3Blue1Brown video](https://www.youtube.com/watch?v=m2MIpDrF7Es), I know better understand this constant.  In this blog post, I will attempt to describe, in my own words, my understanding of Euler's constant and expound on Sanderson's explanation._

Introduction
------------

For many people I've talked to, Euler's constant $e := 2.71828$ is a somewhat mysterious number one is sort of forced to just take for granted. Sadly, it was only very recently that I finally felt like I truly understood this constant. Sure, I knew some _facts_ about $e$, but I didn't really understand its _essence_. For example, I knew that 

$$\frac{de^x}{dx} = 1$$

but did not know why this constant is so ubiqituous. Why, for example, do we choose to represent nearly every logarithm with base $e$? More puzzingly, why do we call this the "natural" logarithm? Why does it appear in the probability density function for the [normal distribution](https://en.wikipedia.org/wiki/Normal_distribution)? Or in [Euler's formula](https://en.wikipedia.org/wiki/Euler%27s_formula)? 

With the help of [Grant Sanderson](Grant Sanderson)'s excellent [3Blue1Brown video](https://www.youtube.com/watch?v=m2MIpDrF7Es), I feel now that I have a much better understanding for it's essence. In this blog post, I will attempt to describe, in my own words, my understanding of Euler's constant and expound on Sanderson's explanation.

To spoil the punchline, Euler's constant is used to express exponential functions -- functions of the form $f(x) := a^x$ -- in a "canonical" way. That is, every function $a^x$ can be expressed as $e^{Kx}$ for some constant $K$. As we will describe, there is good reason to prefer this "canonical" form! Let's dig in.

The essence of exponentials
---------------------------

To review, exponential functions are functions of the form:

$$f(x) := a^x$$

for some constant $a$. Exponential functions are do not only grow, but their _growth_ grows. They look like the following:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/exponential.png" alt="drawing" width="400"/></center>


