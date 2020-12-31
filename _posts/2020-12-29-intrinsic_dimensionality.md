---
title: 'Intrinsic dimensionality'
date: 2020-12-29
permalink: /posts/inverse_matrices/
tags:
  - tutorial
  - mathematics
  - linear algebra
  - matrices
---

THIS POST IS CURRENTLY UNDER CONSTRUCTION

An important concept in linear algebra and the data sciences is the idea of **intrinsic dimensionality**.  I found that in my formal education this concept was never explicitly taught; however, it undergirds so many concepts in linear algebra and data analysis. In this post I will discuss the difference between the **dimensionality** of a space versus its **intrinsic dimensionality**.  This concept provides a nice framework for understanding such broad concepts as the [rank of a matrix](https://en.wikipedia.org/wiki/Rank_(linear_algebra)) in linear algebra as well as [dimension reduction](https://en.wikipedia.org/wiki/Dimensionality_reduction) and [feature selection](https://en.wikipedia.org/wiki/Feature_extraction) in machine learning. 

**What is a space?**

Let's start with a very basic question: what is a space?  According to [Wikipedia](https://en.wikipedia.org/wiki/Space_(mathematics)), a space is a [set](https://en.wikipedia.org/wiki/Set_(mathematics)) of objects with some "structure."  This idea is extremely general, perhaps even trivial to some, but I think it deserves emphasizing that a space is, first and foremost, a *set*.

**Dimensionality**

Let's move on to another basic question: what does it mean for a space to be three-dimensional versus two-dimensional?  More generally, what does it mean for a space to be $D$-dimensional? A basic answer to this question is that a $D$-dimensional space is a space in which one uses $D$ pieces of information to describe each point or object in that space. For example, in three-dimensional space, we need three pieces of information to describe a point: its value along an x-axis, its value along a y-axis, and a value along a z-axis:



**Intrinsic dimensionality**

Let's say we're in some situtation we're we are dealing with points (or objects) in some $D$-dimensional space. Thus, we are dealing with $D$ pieces of information for describing "things" in that space. One may ask a simple question: do we *really* need $D$ pieces of information to describe each thing? Or can we get by with fewer?

Take the following example:
