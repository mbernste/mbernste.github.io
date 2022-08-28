---
title: 'The overloaded equals sign'
date: 2021-11-09
permalink: /posts/equality_definition/
tags:
  - tutorial
  - mathematics
  - pedagogy
---

_Two of the most important relationships in mathematics, namely equality and definition, are both denoted using the same symbol -- namely, the equals sign. The overloading of this symbol confuses students in mathematics and computer programming. In this post, I argue for the use of two different symbols for these two fundamentally different operators._

Introduction
----------

I find it unfortunate that two of the most important relationships in mathematics, namely **equality** and **definition**, are often denoted using the exact same symbol -- namely, the equal sign: "=". Early in my learning days, I believe that this [overloading](https://en.wikipedia.org/wiki/Operator_overloading) of the equal sign led to more confusion than necessary and I have personally witnessed it confuse students.  

To ensure that we're on the same page, let's first define these two notions. Let's start with the idea of **equality**.  Let's say we have two entities, which we will denote using the symbols $X$ and $Y$.  The statement "$X$ equals $Y$", denoted $X = Y$, means that $X$ and $Y$ **are the same thing**.  

For example, let's say we have a right-triangle with edge lengths $a$, $b$ and $c$, where $c$ is the hypotenuse. The [Pythagorean Theorem](https://en.wikipedia.org/wiki/Pythagorean_theorem) says that $a^2 + b^2 = c^2$. Said differently, the quantity $c^2$ *is the same quantity* as the quantity $a^2 + b^2$.

Now, let's move on to **definition**. Given some entity denoted with the symbol $Y$, the statement "let $X$ be $Y$", also often denoted $X = Y$, means that one should use the symbol "$X$" to refer to the entity referred to by "$Y$".  

For example, in introductory math textbooks it is common to define the sine function in reference to a right-triangle: 

$$\sin \theta = \frac{\text{opposite}}{\text{hypotenuse}}$$

This is a definition. We are **assigning** the symbol/concept $\sin \theta$ to be the ratio of the length of the triangle's opposite side to the length of its hypotenuse.

The fundamental difference between equality and definition is that in the the equality relationship between $X$ and $Y$, both the symbols $X$ and $Y$ are bound to entities -- that is, they "refer" to entities. The statement $Y = X$ is simply a comment about those two entities, namely, that they are the same.  In contrast, in a definition, only one of the two symbols is bound to an entity. The act of stating a definition is the act of *binding a known entity to a new symbol*.  For example, the symbol "$\text{foo} \ \theta$" is meaningless. What exactly is "foo"?  We don't know because we have not defined it.

Overloading the equal sign creates confusion in mathematics
-----------------------------------------------------------

I was tutoring someone who was teaching themselves pre-calculus out of a textbook, and they were quite confused by the statement, 

$$\sin \theta = \frac{\text{opposite}}{\text{hypotenuse}}$$

They asked me, "Why is $\sin \theta$ equal to the quantity $\frac{\text{opposite}}{\text{hypotenuse}}$?" They never explicitly stated so, but it become evident that their confusion was not the good kind of confusion. It wasn't, "Why are the ratios between the sides of a right-triangle functions of the angles between those sides?" Nor, "Why is this definition important?"  Rather, their confusion seemed to stem from the very existence of this mysterious object, "$\sin \theta$". Their question was more along the lines of, "What _is_ this mysterious thing? And why on earth is it equal to the ratio of the sides of the triangle?" 

Their confusion arose from the erroneous interpretation of this statement as describing an equality rather than a definition. The mystery was, at least partly, alleviated by the clarification that $\sin \theta$ is not an object that existed before we saw this statement -- rather, this statement _created the object for the first time_. The statement is _defining_ $\sin \theta$ to be the ratio between the opposite side to the hypotenuse. 

The real interesting quality to this definition is that the ratio of the sides of a right triangle are a function of its angles regardless of the lengths of the sides. That is, that we can create this definition at all!

Overloading the equal sign creates confusion in computer programming
--------------------------------------------------------------------

Anyone who has taught introductory computer programming is familiar with the very common confusion between the [assignment operator](https://en.wikipedia.org/wiki/Assignment_(computer_science)) and [equality operator](https://en.wikipedia.org/wiki/Relational_operator#Equality) in programming languages.  

For example, in many programming languages, like C and Python, the assigment operator uses the standard equals sign. That is, the statement `x = y` assigns the value referenced by symbol `y` to symbol `x`.  In contrast, the statement `x == y` returns either `True` or `False` depending on whether the value referenced by `x` is equal to the value referenced by `y`.  Though I have not seen any data on the topic, I wonder whether teaching these two operators from the very beginning of a student's mathematical education would alleviate this common confusion.

Use ":=" instead of "=" to denote definition
--------------------------------------------

I think it's important to use the symbol ":=" to denote definition.  I prefer this symbol over the popular "$\equiv$" symbol because it emphasizes the assymetry of the statement.  That is, $X := Y$ means "use $X$ as a symbol for $Y$", which differs from "use $Y$ as a symbol for $X$." In contrast, the standard equals sign "=" is appropriately symmetric. 

Using the appropriate symbol to distinguish definition statements from equality statements may go a long way, at least in proportion to the effort of using them, towards alleviating confusion in students of math and computer science.  





