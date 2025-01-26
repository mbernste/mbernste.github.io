



Connection to compound interest
-------------------------------

Euler's number was actually discovered first by [Jacob Bernoulli](https://en.wikipedia.org/wiki/Jacob_Bernoulli) as it relates to [compound interest](https://en.wikipedia.org/wiki/Compound_interest). In fact, $e$ is often introduced to students in this way and it's only discussed in relation to exponential functions in more advanced treatments of the topic.

Let us now approach $e$ from the perspective of compound interest and connect it from this perspective back to exponential functions. We'll break apart this explanation into two sections: In the first, we'll derive the formula for continous compound interest, which involves $e$. In the second, we'll tie this formula intuitively back to our discussion of $e$ as being a constant that "describes" all exponential functions.

### A formula for continuous compound interest

Say we have $P$ dollars, as principal, that we lend out at an interest rate $r$ over some unit of time (e.g., one year). After this amount of time, we would have the following amount of money:

$$\begin{align*}\text{Total} &:= P + rP \\ &= P(1+r)  \end{align*}$$

However, because the interest wasn't paid out until the end of the perscribed time, the interest itself was not given the opportunity to earn money. Let's now say that interest is paid out every half unit of time (e.g., every six months instead of every year). Then at the halfway point, when the interest compounds for the first time, the $P$ dollars would earn $\frac{r}{2}P$ and this $\frac{r}{2}P$ could then earn interest for the remaining half of time. We can derive the total amount of money we have left as follows:

Let $P_1$ be the money we have after interest compounds the first time. It compounds at a rate of $r / 2$ because we compounded it at half the time interval (i.e., the first half of time):

$$\begin{align*}P_1 &:= P + \frac{1}{2}P \\ &= P\left(1+\frac{r}{2}\right)  \end{align*}$$

We can calculate the total now by treating $P_1$ as the "principal" starting just after the interest compounds the first time from which it will earn at a rate of $r / 2$ (because it compounds over the second half of time):

$$\begin{align*}P_2 &:= P_1 + \frac{1}{2}P_1 \\ &= P_1\left(1+\frac{r}{2}\right)  \end{align*}$$

Plugging in $P_1$, we get the final total as:

$$\begin{align*} \text{Total} &:= P_2\left( 1+\frac{r}{2} \right) \\ &= P\left(1+\frac{r}{2}\right)\left(1+\frac{r}{2}\right)  \\ &= P\left(1+ \frac{r}{2}\right)^{2} \end{align*}$$

We can play this game again and now instead of compounding twice, it compounds three times. In fact, we can increase the number of times that the money compounds to any arbitrary number, $n$, and we will find that the total we end up with at the end will be:

$$\text{Total} := P\left(1-\frac{r}{n}\right)^n$$

Before we move on, let's generalize this formula slightly and consider the total we would earn after $t$ units of time and derive a formula that takes into account $t$. The derivation will be similar to how we derived the formula above that takes into account the number of times interest compounds per unit of time, $n$. We'll start by considering $t = 2$. Let's let $P_1$ be the interest earned after $t = 1$:

$$\begin{align*}P_1 := P\left(1-\frac{r}{n}\right)^n  \end{align*}$$

Similar to before, we can calculate the total by treating $P_1$ as the "principal" starting after the first unit of time and plugging in $P_1$:

$$\begin{align*}\text{Total} &:= P_1 \left(1-\frac{r}{n}\right)^n \\ &= P\left(1-\frac{r}{n}\right)^n \left(1-\frac{r}{n}\right)^n \\ &= P\left(1-\frac{r}{n}\right)^{2n}\end{align*}$$

We can perform this derivation for any value of $t$ and we would find that 

$$\text{Total} := P\left(1-\frac{r}{n}\right)^{nt}$$

Now that we've generalized our formula to take into account $t$, let's now ask the question: What if we compound the interest _every possible instant --? That is, instead of compounding $n$ times, it compounds an infinite number of times: every possible instant. We can derive this formula by taking the limit of the above formula as $n$ approaches infinity:

$$\begin{align*}\text{Total} &:= \lim_{n \rightarrow \infty} P\left(1-\frac{r}{n}\right)^{tn} \\ &= P \lim_{n \rightarrow \infty} \left(1-\frac{r}{n}\right)^{nt} \\ &= Pe^{rt} && \text{Theorem 1} \end{align*}$$


If we assume that the rate, $r$, is fixed, then we can create a variable $x := rt$ that is a function only of time, $t$. The equation then becomes:

$$\text{Total} = Pe^x$$

This formula is an exponential function! That is, it is an exponential function with respect to the _scaled_ time where the scaling is determined by the rate. Said differently, one can think of $x$ as the number of units of time where each unit is the time it takes to earn 100% of the principal (i.e., double the money). 

### Relating continous compound interest to exponentials

Let's conclude by relating the equation for continuous interest, $\text{Total} = Pe^x$, back to the idea that $e^x$ is the function whose derivative is simply $e^x$. 
