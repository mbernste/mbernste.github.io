
THIS POST IS CURRENTLY UNDER CONSTRUCTION

*The mathematical field of information theory attempts to mathematically describe the concept of “information”. In this series of posts, I will attempt to describe my understanding of how, both philosophically and mathematically, information theory defines the polymorphic, and often amorphous, concept of information. In the first post, we discussed the concept of self-information. In this second post, we will build on this foundation to discuss the concept of information entropy.*

Introduction
-----------

In the [first post] of this series, we discussed how Shannon's Information Theory defines the information content of an event as the degree of surprise that an agent experiences when the event occurs. We discussed how surprise intuitively should correspond to probability in that an event with low probability elicits more surprise because it is unlikely to occur.  Thus, in information theory, information is a function, $I$, called **self-information**, that operates on probability values $p \in [0,1]$:

$$I(p) := -\log p$$

One strange thing about this equation is that it seems to change with respect to the base of the logarithm. Why is that? In this post, we will connect this idea of "information as surprise" to another angle from which we can view information: "information as an efficiency of communication".  This angle starts to take more shape when we introduce the concept of information **entropy**.

Entropy
-----------



