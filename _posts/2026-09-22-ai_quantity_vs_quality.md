---
title: "As AI makes output cheaper, the work of ensuring quality grows"
date: 2026-09-22
permalink: /posts/ai_quantity_quality/
tags:
  - ai
---

_THIS POST IS CURRENTLY UNDER CONSTRUCTION_

_At the time of this writing, September 22, 2026, the gap in quality between the output produced by an AI versus a human expert has still not closed in most domains (coding and math being clear exceptions). In this post, I argue that producing high quality work is still difficult even as AI has made it extremely cheap to produce work at high quantity. For every unit of work produced by an AI, a human is needed to close the quality gap. For this _

Before AI, project planning was mostly about quantity
-----------------------------------------------------

In the old days (all of 8 months ago at the time of this writing), when someone went about planning a project, they would estimate how _big_ of a project they could complete given the resources allocated to them. By "project" here, I mean any kind of knowledge-based product that an individual person or team of people seek to produce: a written article, a computer program, an image, etc. Importantly, the quality of work produced by most experts is often relatively stable. If you ask a professional software engineer, or team of engineers, to create a program, the question would rarely be, "How robust should the program be?" Or, "How clean should the code be?" Rather, the questions would be along the lines of, "What features should this product have?" If you ask a data scientist to perform a data analysis, the question would rarely be, "How correct should these conclusions be?" Instead, it would be more along the lines of, "What questions do we seek to answer?" Depending on how much time is allowed to this person or team, they would estimate what they could accomplish given the constraint.

Because quality, in most cases, is a relatively stable property of the output of human experts, the dimension most often considered during project planning was that of _quantity_. That is, the relationship between effort and quantity was, at a rough pass, linear: The more work I put in, the more stuff I can accomplish. 

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/ai_quantity_only.png" alt="drawing" width="800"/></center>

With AI, project planning is also about quality
-----------------------------------------------

At the time of this writing (September 22, 2026), the gap in quality between the output produced by an AI versus a human expert has still not closed in most domains (coding and math being clear exceptions). Based on my observation, this is because models still lack the nuanced judgement and taste of an expert human being. They often miss the point, write with [unnatural syntax](https://news.ycombinator.com/item?id=49364658), or add unnecessary complexity. That is, without human guidance, much of what they produce is [slop](https://en.wikipedia.org/wiki/AI_slop). 

Unfortunately, closing this quality gap takes a lot of effort! I find this in my own work. As a machine learning scientist and computational biologist, I am now using AI to create analyses, write reports, and create presentations. In my personal experience, the quality of the output is somewhere in the ballpark range of 75% of what I am capable of producing. I find that it takes quite a lot of time to tweak the writing, to remove unnecessary features in its code, to clean its figures, etc. 

The calculus to how we should approach work has completely changed. No longer is _quantity_ the dimension along which we should plan, but rather, it is _quality_. Generating many projects at 75% quality is extremely cheap. But closing the quality gap is still quite expensive. This is illustrated in the schematic below:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/ai_quantity_and_quality.png" alt="drawing" width="800"/></center>

The act of planning a project has become an optimization problem in two dimensions. Producing a large amount of high quality work is extremely expensive because the amount of effort and time it takes to close the quality gap for each unit of work is high. To make this concrete, one must decide whether to produce:

* A lot of work at low quality
* A medium amount of work at medium quality
* A small amount of work at high quality

One must consider two dimensions!

The quality gap explains why humans have more work to do than ever
------------------------------------------------------------------

Moreover, this phenomenon explains why it feels to me like the amount of work we human knowledge workers have to do is higher than ever. For every unit of work produced by an AI, a human has to close the quality gap. Therefore, there are two competing forces: how much _quantity_ AI can produce and how small the _quantity gap_ remains. I predict that no matter how small this quality gap becomes, as the quantity produced by AI becomes cheaper, the amount of work we humans have will increase anyway! The AIs will continue to generate output and ever increasing rates and we humans will have to close the quality gap in each unit of that ever increasing output.

