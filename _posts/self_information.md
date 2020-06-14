
Foundations of information theory (part 1: information as a degree of surprise)

*The mathematical field of information theory attempts to mathematically describe the concept of "information". In this series of posts, I will attempt to describe my understanding of how, both philosophically and mathematically, information theory defines the polymorphic, and often amorphous, concept of information*

Introduction
---------------

Information theory is a mathematical theory for describing "information" invented by the late [Claude Shannon](https://en.wikipedia.org/wiki/Claude_Shannon). Information theory is a fundamental mathematical theory that is tightly woven within any of the data sciences including statistics and machine learning. Thus, it is introduced in many introductory statistics and machine learning courses. 

Strikingly, I found that whenever information theory was taught to me in these courses, the teacher always skipped over what to me seemed to be the most fundamental question of all: what exactly is "information"?  It seemed quite strange to learn a theory without knowing the nature of the subject of that theory!

One reason I think this question is avoided is because we don't really have a good definition for "information." This is evidenced by the fact that there is an [entire field of philosophy](https://plato.stanford.edu/entries/information/) dedicated to the construction of a definition for information.

However, despite the fact that we don't really know what we humans mean by the word "information", information does indeed have a rigorous definition within the mathematical field of information theory. Not only is this definition practically useful, I also find it intellectually satisfying.

Information as a measure of surprise
-----------------

The information theoretic definition for information, often called **self-information**, defines information as an event that elicits "surprise" in the agent that observes the event.  Intuitively, if an event is "surprising", then we gained more information from the event than if the event had been something we were expecting. In essence, a surprising event changes our understanding of the world whereas an expected event supports our current understanding. We see that intuitively “surprise” is a good measure of the information content of a result. Moreover, if an event is "surprising", then presumably, this event is considered unlikely -- that is, to have a low probability of occuring. Thus, the definition for self-information is built upon [probability theory](https://mbernste.github.io/posts/measure_theory_1/).
