
Foundations of information theory (part 1: information as a degree of surprise)

*The mathematical field of information theory attempts to mathematically describe the concept of "information". In this series of posts, I will attempt to describe my understanding of how, both philosophically and mathematically, information theory defines the polymorphic, and often amorphous, concept of information*

Introduction
---------------

Information theory is a mathematical theory for describing "information" invented by the late [Claude Shannon](https://en.wikipedia.org/wiki/Claude_Shannon). Information theory is a fundamental mathematical theory that is tightly woven within any field that can be considered a data science, such as statistics or machine learning. Thus, it is introduced in many introductory college courses. 

Strikingly, I found that whenever information theory was taught to me in these courses, the teacher always skipped over what to me seemed to be the most fundamental question of all: what exactly is "information"?  It seemed quite strange to learn a theory without knowing the nature of the subject of that theory!

One reason I think this question is avoided is because we don't really have a good definition for "information." This is evidenced by the fact that there is an [entire field of philosophy](https://plato.stanford.edu/entries/information/) dedicated to the construction of a definition for information.

However, despite the fact that we don't really know what we humans mean by the word "information", information does indeed have a rigorous definition within the mathematical field of information theory. Not only is this definition practically useful, I also find it intellectually satisfying.

Information as a measure of surprise
-----------------

The information theoretic definition for information, often called **self-information**, defines information as an event that elicits "surprise" in the agent that observes the event.  Intuitively, if an event is "surprising", then we gained more information from the event than if the event had been something we were expecting. In essence, a surprising event changes our understanding of the world whereas an expected event supports our current understanding. We see that intuitively “surprise” is a good measure of the information content of a result. Moreover, if an event is "surprising", then presumably, this event is considered unlikely -- that is, to have a low probability of occuring. Thus, the definition for self-information is built upon [probability theory](https://mbernste.github.io/posts/measure_theory_1/).

From this description, we can think of self-information to be a function $I$ that acts on probabilities. Moreover, if we have a probability of an event $p$ that is low, then if this event occurred, we would be surprised. Thus, $I(p)$ should have a high self-information.

There are other properties that we would like $I$ to have. To state them all:
1. $I$ should be a continuous function. That is since $p \in [0, 1]$, we would like $I$'s domain to be continuous in the interval $[0,1]$. 
2. $I$ should be non-negative. Intuitively, the idea of "negative surprise" does not make much sense. Either we aren't surprised at all, and $I(p) = 0$, or we are surprised and thus $I(p) > 0$.
3. Self-information should be monotonic. As we described before if we have two probabilities $p_1$ and $p_2$ for which $p_1 < p_2$, then the event associated with $p_1$ would be more surprising and thus:

$$p_1 < p_2 \implies I(p_1) > I(p_2)$$

4. If an event has probability 1, then the event is certain to occur and we aren't surprised at all of its occurance. Thus, 

$$I(1) = 0$$

5. The suprise elicited from two independent events should be the sum of the two surprises. Intuitively, if one event occurs, it should not affect the surprise from the other event occuring because, after all, the two events are statistically independent. Thus, given two independent events with probabilities $p_1$ and $p_2$, it should follow that

$$I(p_1p_2) = I(p_1) + I(p_2)$$



