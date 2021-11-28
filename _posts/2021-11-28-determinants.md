---
title: 'Demystifying determinants'
date: 2021-11-28
permalink: /posts/determinants/
tags:
  - tutorial
  - mathematics
  - linear algebra
---


_THIS POST IS CURRENTLY UNDER CONSTRUCTION_

Introduction
------------

Of all of the topics taught in introductory linear algebra, I found the **determinant** to be one of the most confusing. When introduced to determinants, one is taught that the determinant of a matrix $\boldysmbol{A}$ is the area of the parallelapiped formed by columns of $\boldsymbold{A}$. For example, if $\boldysmbol{A}$ is a 2x2 matrix, we can depict the area as follows:


Furthermore, for a 2x2 matrix, this area can be computed via:

$$\text{Det}(\boldsymbol{A}) := ac - bd$$

We can verify this pretty easily geometrically:


So far, this isn't so confusing, but things get worse when you move to higher dimensions. Specifically, it turns out that the determinant for a $m \times m$ matrix $\boldsymbol{A}$ is defined as follows:

$$\text{Det}(\boldsymbol{A}) := \sum_{i \in S_m}$$

If you're like me, this equation is very opaque. How on earth does this calculate the volumne of a m-dimensional parallelapiped? 

In this post, I am going to attempt to demystify this definition. To do so, we will begin with a set of axioms that seek to define the notion of "volume" in an m-dimensional space. From this axiomization, we derive the equation for the determinant above!

Abstracting the concept of volume: the axioms for a determinant
---------------------------------------------------------------

The definition of a determinant does not actually start with the calculation of of volume in the usual sense, but rather, we will start in a more abstract place: axiomizing the properties that "volume" should have. 

**1. The determinant of the identity matrix is one**  

This makes intuitive sense: the parallelopided formed by the columns of the identity matrix form a hypercube in $m$-dimensional space. The volume of a cube is simply the product of the sides of the cube; in this case, they're all of length one so the volume should be one:

That is, we have 

$$\text{Det}(\boldsymbol{I}) = 1$$

**2. If two columns of a matrix are equal, then its determinant is zero**  

First, let's consider what we mean by "volume" in an m-dimensional space. To illustrate volume, let's consider the cube


Deriving the formula for a determinant
--------------------------------------

What is meant by "signed volume"?
---------------------------------
