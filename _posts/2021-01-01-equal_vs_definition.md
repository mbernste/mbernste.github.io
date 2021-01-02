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

I find it a little bit unfortunate that two of the most important relationships in mathematics, namely **equality** and **definition**, are often denoted using the exact same symbol: the equal sign ("="). Early in my learning days, I believe that this [overloading](https://en.wikipedia.org/wiki/Operator_overloading) of the equal sign led to way more confusion than necessary.  In fact, I believe I still have some residual confusion regarding many basic mathematical concepts that all originate from this unfortunate circumstance.  I am almost surely not the first person to point this out, but after a cursory Google search, I could not find an essay or article that expressed the nuance of my concern, so here I'll lay out it and also propose a remedy.

To ensure that we're on the same page, let's first define these two different relationships. Let's start with idea of **equality**.  Let's say we have two entities, which we will denote using the symbols $X$ and $Y$.  The statement "$X$ equals $Y$", denoted $X = Y$, means that $X$ and $Y$ **are the same thing**.  

For example, let's say we have a right-triangle with edge lengths $a$, $b$ and $c$, where $c$ is the hypotenuse: 


The [Pythagorean Theorem](https://en.wikipedia.org/wiki/Pythagorean_theorem) says that $a^2 + b^2 = c^2$. Said differently, the quantity $c^2$ *is the same quantity* as the quantity $a^2 + b^2$.

Now, let's move on to **definition**. Given some entity denoted with the symbol $Y$, the statement "let $X$ be $Y$", also often denoted $X = Y$, means that one should use the symbol "$X$" to refer to the entity referred to by "Y".  For example, in textbooks it is common to define the sine function for a right triangle as 

$$\sin \theta = \frac{\text{opposite}}{\text{hypotenuse}}$$

This is a definition. We are **assigning** the symbol/concept $\sin \theta$ to be the ratio of the length of the triangle's opposite side to the length of its hypotenuse.

The fundamental difference between equality and definition
----------------

The fundamental difference between equality and definition is that in the the equality relationship between $X$ and $Y$, both the symbols $X$ and $Y$ are bound to entities -- that is, they "refer" to entities. The statement $Y = X$ is simply a comment about those two entities, namely, that they are the same.

In contrast, in a definition, only one of the two symbols is bound to an entity. The act of stating a definition is the act of *binding a known entity to a new symbol*.  For example, the symbol "$\text{foo} \ \theta$" is meaningless. What exactly is "foo"?  We don't know because we have not defined it.

Overloading the equal sign creates confusion
----------------

Here's a story to illustrate how the overloading of the equal symbol creates confusion. My mom is a very curious person and over the last year, she has set out to (re)learn high school math and physics. It has been decades since she has seen the material, but she is steadily plugging away through pre-calculus and kinematics. She was quite confused when she came upon the statement, 

$$\sin \theta = \frac{\text{opposite}}{\text{hypotenuse}}$$

She asked, why is $\sin \theta$ equal to the quantity $\frac{\text{opposite}}{\text{hypotenuse}}$? It was as if $\sin \theta$ were this utterly mysterious object that somehow, magically, is equal to the ratio of the length of the opposite side to the length of the hypotenuse. Her confusion arose from her erroneous interpretation of this statement as describing an equality -- i.e., "these two quantities, $\sin \theta$ and $\frac{\text{opposite}}{\text{hypotenuse}}$, are the same" -- when it was meant to describe a definition: "$\sin \theta$ is defined to be the quantity $\frac{\text{opposite}}{\text{hypotenuse}}$". 

Of course, there is still a little bit of mystery left in $\sin \theta$. One may ask, why would we ever care to create such a definition. To which one could then answer that *all* right triangle that have the angle $\theta$ between one of its sides and the hypotenuse would have the same ratio of the length of the opposite side to the length of the hypotenuse.  That is, this ratio will *always* be the same quantity for any right triangle so long as the angle is the same.  For some angle $\theta$, we denote this shared ratio as "$\sin \theta$". 

Use ":=" instead of "=" for definitions
----------------

I think it's important to use the symbol ":=" to denote definition.  I prefer this symbol over the popular "$\equiv$" symbol because it emphasizes the assymetry of the statement.  That is, $X := Y$ means "use $X$ as a symbol for $Y$", which differs from "use $Y$ as a symbol for $X$." In contrast, the plain equal sign "=" is appropriately symmetric. 

Using the appropriate symbol to distinguish definition statements from equality statements may go a long way, at lesat in proportion to the effort, towards alleviating confusion with novice readers.  





