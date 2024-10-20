---
title: 'Denoising diffusion probabilistic models (Part 2: Theoretical justification)'
date: 2024-10-20
permalink: /posts/diffusion_part2/
tags:
  - tutorial
  - deep learning
  - machine learning
  - probabilistic models
---

_THIS POST IS CURRENTLY UNDER CONSTRUCTION_


Introduction
------------

In [Part 1](https://mbernste.github.io/posts/diffusion_part1/) of this series, we introduced the denoising diffusion probabilistic model for modeling and sampling from complex distributions. As a brief review, diffusion models learn how to reverse a diffusion process. Specifically, given a data object $\boldsymbol{x}$, this diffusion process iteratively adds noise to $\boldsymbol{x}$ until it becomes pure white noise. The goal of a diffusion model is to learn to reverse this diffusion process via a model $p_\theta$ parameterized by parameters $\theta$: 

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/diffusion_example_korra_forward_reverse_distributions_approximate.png" alt="drawing" width="800"/></center>

Once we have this model in hand, we can generate an object by first sampling white noise $\boldsymbol{x}\_T$ from a standard normal distribution $N(\boldsymbol{0}, \boldsymbol{I})$, and then iteratively sampling $\boldsymbol{x}\_{t-1}$ from each learned $p\_{\theta}(\boldsymbol{x}\_{t-1} \mid \boldsymbol{x}\_{t})$ distribution. At the end of this process we will have "transformed" the random white noise into an object.

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/diffusion_example_generation_korra.png" alt="drawing" width="800"/></center>

To learn this model, we will fit the joint distribution given by the reverse-diffusion model, $p\_{\theta}(\boldsymbol{x}\_{0:T})$, to joint distribution given by the forward-diffusion model, $q(\boldsymbol{x}\_{0:T})$. Specifically, we will seek to minimize the KL-divergence from $p\_\theta(\boldsymbol{x}\_{0:T})$ to $q(\boldsymbol{x}\_{0:T})$:

$$\hat{\theta} := \text{arg min}_\theta \ KL( q(\boldsymbol{x}_{0:T}) \ \vert\vert \ p_\theta(\boldsymbol{x}_{0:T}))$$

While the core idea of learning a denoising model that reverses a diffusion process and then using that denoising model to produce samples may be intuitive at a high-level, one may be wanting for a more rigorous theoretical motivation for the objective function that entails fitting $p_\theta(\boldsymbol{x}\_{0:T})$ to $q(\boldsymbol{x}\_{0:T})$ by minimizing their KL-divergence.  That is, recall that the goal in traditional probabilistic modeling is fit a model $p_\theta(\boldsymbol{x}_0)$ that approximates the real-world, unknown distribution $q(\boldsymbol{x}_0)$. How does fitting a model to a reverse a diffusion lead accompish this task? Furthermore, what traditional statistical inference frameworks is this related to?

In this post we will answer these questions by discussing several [perspectives](https://mbernste.github.io/posts/understanding_3d/) to motivate and understand the diffusion model objective. Specifically, we will view this objective in the following ways:

1. As maximum-likelihood estimation
2. As implicitly minimizing an upper bound on the KL-divergence between $q(\boldsymbol{x}\_0)$ and $p_\theta(\boldsymbol{x}\_0)$
3. As training a hierarchical variational autoencoder that uses a parameterless inference model
4. As score-matching
5. As breaking up a difficult problem into many easier problems

Let's go through each of them.

## 1. As maximum-likelihood estimation

Our reverse diffusion process can be thought about as a model, like any other, over noiseless objects $\boldsymbol{x}_0$, which we can access by marginalizing over all of the intermediate objects $\boldsymbol{x}\_{1:T}$:

$$p_\theta(\boldsymbol{x}_0) = \int p(\boldsymbol{x}_0, \boldsymbol{x}_{1:T}) \ d\boldsymbol{x}_{1:T}$$

It turns out that minimizing the KL-divergence from $p_\theta(\boldsymbol{x}\_{0:T})$ to $q(\boldsymbol{x}\_{0:T})$ can be viewed as doing approximate [maximum likelihood esimation](https://en.wikipedia.org/wiki/Maximum_likelihood_estimation). 

To see why, remember how we showed that minimizing the KL-divergence from $p_\theta(\boldsymbol{x}\_{0:T})$ to $q(\boldsymbol{x}\_{0:T})$ could be accomplished implicitly by maximizing the ELBO:

$$\begin{align*}\hat{\theta} &:= \text{arg max}_\theta \ \text{ELBO}(\theta) \\ &= \text{arg max}_\theta \  E_{\boldsymbol{x}_{1:T} \mid \boldsymbol{x}_0 \sim q}\left[ \log\frac{p_\theta (\boldsymbol{x}_{0:T}) }{q(\boldsymbol{x}_{1:T} \mid \boldsymbol{x}_0) } \right]\end{align*}$$

Notice that if we maximize the ELBO, we are not only minimizing the KL-divergence (our original stated goal), but we are also implicitly maximizing a lower bound of the log-likelihood, $\log p_\theta(\boldsymbol{x})$. That is, we see that 

$$\begin{align*} \log p_\theta(\boldsymbol{x}) &= KL( q(\boldsymbol{x}_{1:T} \mid \boldsymbol{x}_0) \ \vert\vert \ p_\theta(\boldsymbol{x}_{1:T} \mid \boldsymbol{x}_0)) + \underbrace{E_{\boldsymbol{x}_{1:T} \mid \boldsymbol{x}_0 \sim q} \left[ \log\frac{p_\theta (\boldsymbol{x}_{0:T}) }{q(\boldsymbol{x}_{1:T} \mid \boldsymbol{x}_0) } \right]}_{\text{ELBO}} \\ &\geq  \underbrace{E_{\boldsymbol{x}_{1:T} \mid \boldsymbol{x}_0 \sim q}\left[ \log\frac{p_\theta (\boldsymbol{x}_{0:T}) }{q(\boldsymbol{x}_{1:T} \mid \boldsymbol{x}_0) } \right]}_{\text{ELBO}} \ \ \text{Because KL-divergence is non-negative} \end{align*}$$

This idea is depicted schematically below (this figure is adapted from [this blog post by Jakub Tomczak](https://jmtomczak.github.io/blog/4/4_VAE.html)):

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/ELBO_vs_log_likelihood.png" alt="drawing" width="600"/></center>

Here, $\theta^\*$ represents the maximum likelihood estimate of $\theta$ and $\hat{\theta}$ represents the value for $\theta$ that maximizes the ELBO. If this lower-bound is tight, $\hat{\theta}$ will be close to $\hat{\theta}$. Although in most cases, it is difficult to know with certainty how tight this lower bound is, in practice, this strategy of maximizing the ELBO leads to good results at estimating $\theta^\*$.

## 2. As implicitly minimizing an upper bound on the KL-divergence between $q(\boldsymbol{x}\_0)$ and $p\_\theta(\boldsymbol{x}\_0)$

Recall that our ultimate goal in fitting a denoising diffusion model is to fit a model $p_\theta(\boldsymbol{x}_0)$ that approximates the real-world, unknown distribution $q(\boldsymbol{x}_0)$. As we described in the previous section, $p_\theta(\boldsymbol{x}_0)$ can be obtained by marginalizing over all of the intermediate objects $\boldsymbol{x}\_{1:T}$. 

As explained eloquently by Alexander Alemi in [his blog post on this topic](https://blog.alexalemi.com/diffusion.html#extra-entropy), by minimizing the KL-divergence between the full diffusion process's joint distributions, $p\_\theta(\boldsymbol{x}\_{0:T})$ and $q(\boldsymbol{x}\_{0:T})$, we will implicitly minimize an upper bound on the KL-divergence from $p\_\theta(\boldsymbol{x}\_0)$ to $q(\boldsymbol{x}\_0)$ (See Derivation 1 in the Appendix to this post): 

$$KL(q(\boldsymbol{x}_{0:T}) \ \vert\vert \ p_\theta(\boldsymbol{x}_{0:T})) \geq KL(q(\boldsymbol{x}_0) \ \vert\vert \ p_\theta(\boldsymbol{x}_0)) \geq 0$$

Thus, by minimizing $KL(q(\boldsymbol{x}\_{0:T}) \ \vert\vert \ p_\theta(\boldsymbol{x}\_{0:T}) )$, we are implicitly learning to fit $p\_\theta(\boldsymbol{x}\_0)$ to $q(\boldsymbol{x}_0)$! 

## 3. As training a hierarchical variational autoencoder that uses a parameterless inference model

Though this does beg the question, why don't we fit $p\_\theta(\boldsymbol{x}\_0)$ to $q(\boldsymbol{x}\_0)$ directly? To answer this, let us remind ourselves that it is often a fruitful strategy to posit a latent generative process of the observed data and try to fit a model of that latent, generative process rather than fit the marginal distribution of the observed data directly. As we will discuss in the next section (Perspective 3), the idea of expanding the model from modeling a distribution over only a random variable representing the data, $\boldsymbol{x}\_0$, to extra random variables involved in a complex generative process, $\boldsymbol{x}\_{1:T}$, we implicitly posit a latent variable model of the observed data. That latent variable model resembles a [variational autoencoder (VAE)](https://mbernste.github.io/posts/vae/)! 

As a brief review, recall that in the VAE framework, we assume that every data item/object that we wish to model, $\boldsymbol{x}$, is associated with a latent variable $\boldsymbol{z}$. We specify an inference model, $q\_\phi(\boldsymbol{z} \mid \boldsymbol{x})$, that approximates the posterior distribution $p\_\theta(\boldsymbol{z} \mid \boldsymbol{x})$. Note that $q\_\phi(\boldsymbol{z} \mid \boldsymbol{x})$ is parameterized by a set of parameters $\phi$. One can view $q\_\phi(\boldsymbol{z} \mid \boldsymbol{x})$ as a sort of _encoder_; given a data item $\boldsymbol{x}$, we encode it into a lower-dimensional vector $\boldsymbol{z}$. We also specify a generative model, $p\_\theta(\boldsymbol{x} \mid \boldsymbol{z})$, that given a lower-dimensional, latent vector $\boldsymbol{z}$, we can generate $\boldsymbol{x}$ by sampling. If we have encoded $\boldsymbol{x}$ into $\boldsymbol{z}$, sampling from the distribution $p\_\theta(\boldsymbol{x} \mid \boldsymbol{z})$ will produce objects that resemble the original $\boldsymbol{x}$. Thus $p\_\theta(\boldsymbol{x} \mid \boldsymbol{z})$ can be viewed as a _decoder_. This process is depicted schematically below:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/diffusion_VAE_graphical_model.png" alt="drawing" width="170"/></center>

<br>

Now, compare this setup to the setup we have described for the diffusion model:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/diffusion_graphical_model_like_VAE.png" alt="drawing" width="400"/></center>

These figures were adapted from [this blog post](https://angusturner.github.io/generative_models/2021/06/29/diffusion-probabilistic-models-I.html) by Angus Turner.

In the case of a diffusion model, we have an observed item $\boldsymbol{x}_0$ that we iteratively corrupt into $\boldsymbol{x}_T$. In a way, we can view $\boldsymbol{x}_T$ as a latent representation associated with $\boldsymbol{x}_T$ in a similar way that $\boldsymbol{z}$ is a latent representation of $\boldsymbol{x}$ in the VAE. Note that this is a "hierarchical" VAE since we do not associate a single latent variable with each $\boldsymbol{x}_0$, but rather a whole sequence of latent variables $\boldsymbol{x}_1, \dots, \boldsymbol{x}_T$.

Moreover, the training objectives between the traditional VAE and this "hierarchical" VAE are identical. In the case of the traditional VAE, our goal is to minimize the KL-divergence from $p\_\theta(\boldsymbol{z} \mid \boldsymbol{x})$ to $q\_\phi(\boldsymbol{z} \mid \boldsymbol{x})$:

$$\hat{\theta}, \hat{\phi} := \text{arg max}_{\theta, \phi} \ KL(q_\phi(\boldsymbol{z} \mid \boldsymbol{x}) p_\theta(\boldsymbol{z} \mid \boldsymbol{x}))$$

In the case of the diffusion model,  we seek to minimize the KL-divergence from $p_\theta(\boldsymbol{x}\_0, \dots, \boldsymbol{x}\_T)$ to $q_(\boldsymbol{x}_0, \dots, \boldsymbol{x}\_T)$


## 4. As score matching

Another motivation for diffusion models lies in their connection to [score matching models](https://arxiv.org/abs/1907.05600). While we will not go into great depth in this blog post (we will merely touch upon it), as it turns out, we will work out a form of the ELBO that can be viewed as an objective function that estimates the _score function_ of the true, real-world distribution $q(\boldsymbol{x}\_0))$.

As a brief review, the _score function_, $s(\boldsymbol{x})$, of the distribution $q(\boldsymbol{x}))$ is simply, 

$s_q(\boldsymbol{x}) := \nabla_{\boldsymbol{x}} \log q(\boldsymbol{x})$

That is, it is the gradient of the log-density function, $q(\boldsymbol{x})$, with respect to the data. Below, we depict a hypothetical density function, $q(\boldsymbol{x})$, and the [vector field](https://en.wikipedia.org/wiki/Vector_field#:~:text=In%20vector%20calculus%20and%20physics,a%20point%20on%20the%20plane.) defined by $\nabla_{\boldsymbol{x}} \log q(\boldsymbol{x})$ below it:

<br>

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/diffusion_score.png" alt="drawing" width="300"/></center>

<br>

Stated more succintly, by maximizing the ELBO with respect to $\theta$ (that is, a lower bound of the log-likelihood), we are also implicitly fitting an estimated score function $s\_\theta(\boldsymbol{x})$ to the real score function $s\_q(\boldsymbol{x})$. We will make this connection more explicit later in the blog post.

Finally, it will turn out that we can view the process of reversing the diffusion process to sample from $p\_\theta(\boldsymbol{x}_0)$ as a variant of [sampling via Langevin dynamics] -- a stochastic method that enables one to sample from an arbitrary distribution by following the gradients defined by the score function.

## 5. As breaking up a difficult problem into many easier problems

Another, more high-level, reason why diffusion models tend to perform better than other methods, such as [variational autoencoders](https://mbernste.github.io/posts/vae/), is that diffusion models break up a difficult problem into a series of easier problems. That is, unlike variational autoencoders, where we train a model to produce an object all at once, in diffusion models, we train the model to produce the object step-by-step. Intuitively, we train a model to "sculpt" an object out of noise in a step-wise fashion rather than generate the object in one fell-swoop. 

This step-wise approach is advantageous because it enables the model to learn features of objects at different levels of resolution. At the end of the reverse diffusion process (i.e., the sampling process), the model identifies broad, vague features of an object within the noise. At later steps of the reverse diffusion process, it fills in smaller details of the object by removing the last remaining noise.

## Appendix

### Derivation 1 (Deriving an upper bound over $KL(q(\boldsymbol{x}\_0) \ \vert\vert \ p\_\theta(\boldsymbol{x}\_0)))$:

$$\begin{align*}KL(q(\boldsymbol{x}_{0:T}) \ \vert\vert \ p_\theta(\boldsymbol{x}_{0:T})) &= E_{\boldsymbol{x}_{0:T} \sim q} \left[ \log \frac{q(\boldsymbol{x}_{0:T})}{p_\theta(\boldsymbol{x}_{0:T})} \right] \end{align*} \\ &= E_{\boldsymbol{x}_{0:T} \sim q} \left[ \log \frac{q(\boldsymbol{x}_{1:T} \mid \boldsymbol{x}_0)q(\boldsymbol{x}_0)}{p_\theta(\boldsymbol{x}_{1:T} \mid \boldsymbol{x}_0)p_\theta(\boldsymbol{x}_0)} \right] \\ &= E_{\boldsymbol{x}_{0:T} \sim q} \left[ \log \frac{q(\boldsymbol{x}_{1:T} \mid \boldsymbol{x}_0)}{p_\theta(\boldsymbol{x}_{1:T} \mid \boldsymbol{x}_0)} \right] + E_{\boldsymbol{x}_{0} \sim q} \left[ \log \frac{q(\boldsymbol{x}_0)}{p_\theta(\boldsymbol{x}_0)} \right]$$

$$= E_{\boldsymbol{x}_0 \mid q} \left[ E_{\boldsymbol{x}_{1:T} \mid \boldsymbol{x}_0 \sim q} \left[ \log \frac{q(\boldsymbol{x}_{1:T} \mid \boldsymbol{x}_0)}{p_\theta(\boldsymbol{x}_{1:T} \mid \boldsymbol{x}_0)} \right]\right] + E_{\boldsymbol{x}_{0} \sim q} \left[ \log \frac{q(\boldsymbol{x}_0)}{p_\theta(\boldsymbol{x}_0)} \right]$$

$$= E_{\boldsymbol{x}_0} \left[ KL(q(\boldsymbol{x}_{1:T} \mid \boldsymbol{x}_0) \ \vert\vert \ p_\theta(\boldsymbol{x}_{1:T} \mid \boldsymbol{x}_0)) \right] + KL(q(\boldsymbol{x}_0) \ \vert\vert \ p_\theta(\boldsymbol{x}_0))$$

$$\geq KL(q(\boldsymbol{x}_0) \ \vert\vert \ p_\theta(\boldsymbol{x}_0))$$

The inequality follows from the fact that KL-divergence is always positive.

