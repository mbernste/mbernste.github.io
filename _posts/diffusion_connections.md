


I have found [three different perspectives](https://mbernste.github.io/posts/understanding_3d/) from which one can understand how diffusion models both represent and learn a distribution,  $p(\boldsymbol{x})$:

1. As a model that learns how to reverse a [diffusion process](https://en.wikipedia.org/wiki/Diffusion_process#:~:text=In%20probability%20theory%20and%20statistics,many%20real%2Dlife%20stochastic%20systems.)
2. As a hierarchical [variational autoencoder](https://mbernste.github.io/posts/vae/)
3. As a [score matching model](https://yang-song.net/blog/2021/score/)

In this first of three blog posts, I will present my understanding of diffusion models through the first of these perspectives. This will entail deriving 

these three perspectives. 
