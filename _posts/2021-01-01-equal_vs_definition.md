---
title: 'Equality vs. definition: An important distinction'
date: 2020-12-29
permalink: /posts/equality_definition/
tags:
  - tutorial
  - mathematics
  - pedagogy
---

THIS POST IS CURRENTLY UNDER CONSTRUCTION

Introduction
----------

I find it pretty strange that two of the most important relationships in mathematics, namely **equality** and **definition**, are denoted using the exact same symbol: the equal sign, "=". Early in my learning days, I believe that this [overloading](https://en.wikipedia.org/wiki/Operator_overloading) of the equal sign led to way more confusion than necessary.  In fact, I believe I still have some residual confusion regarding many basic mathematical concepts that all originate from this unfortunate circumstance.  I am almost surely not the first person to point this out, but after a cursory Google search, I could not find an essay or article that expressed the nuance of my concern, so here I'll lay out it and also propose a remedy.

To ensure that we're on the same page, let's first define these two different relationships. Let's start with idea of **equality**.  Let's say we have two entities, which we will denote using the symbols $X$ and $Y$.  The statement "$X$ equals $Y$", denoted $X = Y$, means that $X$ and $Y$ **are the same thing**.  

For example, let's say we have a right-triangle with edge lengths $a$, $b$ and $c$, where $c$ is the hypotenuse: 


The [Pythagorean Theorem](https://en.wikipedia.org/wiki/Pythagorean_theorem) says that $a^2 + b^2 = c^2$. Said differently, the quantity $c^2$ *is the same quantity* as the quantity $a^2 + b^2$.

Now, let's move on to **definition**. Given some entity denoted with the symbol $Y$, the statement "let $X$ be $Y$" is also denoted as $X = Y$.  For example, given the same right triangle with edge lengths $a$, $b$, and $c$, where we now we let $\theta$ be the angle between the hypotenuse and the edge whose length is $a$, we define the quantity $\sin \theta$ as the $\frac{b}{c}$.  That is,

$$\sin \theta = \frac{b}{c}$$

This is a definition. We are **assigning** the symbol/concept $\sin \theta$ to be the quantity $\frac{b}{c}$.

The fundamental difference between equality and definition
----------------

The fundamental difference between equality and definition is that in the the equality relationship between $X$ and $Y$, both the symbols $X$ and $Y$ are bound to entities -- that is, they "refer" to entities. The statement $Y = X$ is simply a comment about those two entities, namely, that they are the same.

In contrast, in a definition, only one of the two symbols is bound to an entity. The act of stating a definition is the act of *binding a known entity to a new symbol*.  For example, the symbol "$\text{foo} \ \theta$" is meaningless. What exactly is "foo"?  We don't know because we have not defined it.

Overloading the equal sign creates confusion
----------------

Here's a story to illustrate how the overloading of the equal symbol creates confusion. My mom is a very curious person and over the last year, she has set out to (re)learn high school math and physics. It has been decades since she has seen the material, but she is steadily plugging away through pre-calculus and kinematics. Moreover, she doesn't just want to know the material, she wants to *really* know the material. She wants to know the essence of each concept. 

She was quite confused when she came upon the statement, 

$$\sin \theta = \frac{\text{opposite}}{{hypotenuse}}$$

She asked, *why* is $\sin \theta$ *equal* to the quantity $\frac{\text{opposite}}{{hypotenuse}}$? She was interpreting this phrase to be an equality: "these two quantities, $\sin \theta$ and $\frac{b}{c}$, are the same." Instead, the statement should read, $\sin \theta$ is assigned to be the fraction $\frac{\text{opposite}}{{hypotenuse}}$. Really, what this statement says is that for *any* right triangle with an angle $\theta$, the ratio of the length of the opposite side of the angle to the length of the hypotenuse is *always* the same quantity no matter what the lengths actually are (it's just a natural fact about right triangles). This ratio for the angle $\theta$ is denoted $\sin \theta$. 

Equality vs. definition when defining probabalistic models
----------------

In retrospect, the overloading of the equal sign to denote both equality and definition was a source of confusion early in grad school when I began learning more about probabilistic modeling. The confusion stems from the fact that, in some cases, one builds a probabilistic model by defining a joint distribution over multiple random variables and then deriving each variables marginal distribution. For example, for two random variables $X$ and $Y$ that are jointly distributed according to a multivariate normal distribution, we would say that 

$$p(X, Y) = $$

This is a definition. We are defining how to assign probabilities to joint assignments of $X$ and $Y$. Then, the marginal distribution of, say, $X$ is then 

$$p(X) = $$

This is an equality. The quantity $p(X)$ is the same quantity as the left-hand side.

In other cases, especially when the variables are independent (or conditionally independent on some other variables), one can first define distributions over individual random variables or on conditional random variables and then derive their joint distribution.  

":=" instead of "="
----------------

I'm a big fan of the symbol ":=" to denote definition. I prefer this symbol to the symbol "". 





