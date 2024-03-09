## Variational Inference: First Principles
From Bayes' theorem, we set up the problem: 

$p(z|x;\theta)=\frac{p(x|z;\theta)p(z;\theta)}{p(x;\theta)}$

Which just reinforces that the posterior is proportional to the likelihood times the prior. Note that $p(x;\theta)=\int p(x|z;\theta)p(z;\theta) \, dz$ is the evidence, which can bear a very high dimensionality (might be intractable). This is *no bueno* and is the source of many headaches, but also some cool algorithms. 

Variational inference seeks to give better approximations when our posterior density is not so tractable. 

Let me make your life worse by presenting a set of local variational parameters $\phi_{i}$ which belong to $q(z|x_{i};\phi_{i})$. This pretty much says that the latent distribution of vector $z$ (given $i$ observations) is equipped by local parameters. Now, given that we have global parameters $\theta$, we could possibly update each $\phi_{i}$ upon each successive observation. As we update, we can get closer and closer to our global $\theta$. More on this later.

One of the central approaches to tackling this optimization problem is through the Kullback-Leibler (KL) divergence. Horribly informalized, it is the measure between our approximating distribution $q(z)$ and the true density $p(z)$. Now, we have the objective function:

$\mathcal{C}=\sum^{N}_{i=1}D_{KL}(q(z|x_{i};\phi_{i})\ ||\ p(z|x_{i};\theta))$ 

where $D_{KL}=\mathbb{E}_{q}[\log q(z|x_{i};\phi_{i})-\log p(z|x_{i};\theta)]$

Which is just the expectation w.r.t. $q$ of the difference between the log densities.
However, taking the expectations of a forward $D_{KL}$  does not yield a closed form. So we turn to approximations. 


The mean field approximation assumes that our variational posterior is fully factorizable

$\displaystyle q(z_{1},\dots,z_{N})=\prod^{N}_{k=1}q(z_{k})$

by partitioning elements of $z$ into disjoint groupings $z_{k}$.


