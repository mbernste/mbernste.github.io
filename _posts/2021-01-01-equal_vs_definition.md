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

It sometimes amazes me that two of the most important relationships in mathematics, namely **equality** and **definition**, are denoted using the exact same symbol: the equal sign, "=". Early in my learning days, I believe that this [overloading](https://en.wikipedia.org/wiki/Operator_overloading) of the equal sign led to way more confusion than necessary.  In fact, I believe I still have some residual confusion regarding many basic mathematical concepts that all originate from this unfortunate circumstance.  I am almost surely not the first person to point this out, but after a cursory Google search, I could not find an essay or article that expressed the nuance of my concern, so here I'll lay out it and also propose a remedy.

To ensure that we're on the same page, let's first define these two different relationships. Let's start with idea of **equality**.  Let's say we have two entities, which we will denote using the symbols $X$ and $Y$.  The statement "$X$ equals $Y$", denoted $X = Y$, means that $X$ and $Y$ **are the same thing**.  Here's an example: given a right-triangle with edge lengths $a$, $b$ and $c$, where $c$ is the hypotenuse, it holds that $a^2 + b^2 = c^2$:



This is the [Pythagorean Theorem](https://en.wikipedia.org/wiki/Pythagorean_theorem).  Importantly, what this says is that the quantity $c^2$ *is the same quantity* as the quantity $a^2 + b^2$.

Now, let's move on to **definition**. Given some entity denoted with the symbol $Y$, the statement "let $X$ be $Y$" is also denoted as $X = Y$.  For example, given the same right triangle with edge lengths $a$, $b$, and $c$, where we now we let $\theta$ be the angle between the hypotenuse and the edge whose length is $a$, we define the quantity $\sin \theta$ as the $\frac{b}{c}$.  That is,

$$\sin \theta = \frac{b}{c}$$

This is a definition. We are **assigning** the symbol/concept $\sin \theta$ to be the quantity $\frac{b}{c}$.

The fundamental difference between equality and definition
----------------

The fundamental difference between equality and definition is that in the the equality relationship between $X$ and $Y$, both the symbols $X$ and $Y$ are bound to entities -- that is, they "refer" to entities. The statement $Y = X$ is simply a comment about those two entities, namely, that they are the same.

In contrast, in a definition, only one of the two symbols is bound to an entity. The act of stating a definition is the act of *binding a known entity to a new symbol*.  For example, the symbol "$\text{foo} \ \theta$" is meaningless. What exactly is "foo"?  We don't know because we have not defined it.

Overloading the equal sign creates confusion
----------------

To illustrate how the overloading of the equal sign creates confusion, I'll tell a personal story. My mom is a very curious person and over the last year, she has set out to (re)-learn high school level math and physics. It has been decades since she has seen trigonometric identities, but now she wants to learn about them. She *really* wants to learn about them. What *are* they?  

When she came to the phrase, $\sin \theta = \frac{b}{c}$, she was quite confused. She wanted to know *why* $\sin \theta$ is *equal* to the quantity $\frac{b}{c}$.  What magic is happening inside of $\sin \theta$ that enables it to be $\frac{b}{c}?




