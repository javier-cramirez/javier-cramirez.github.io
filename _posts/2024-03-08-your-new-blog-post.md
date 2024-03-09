## Variational Inference: First Principles
<script>
MathJax = {
  tex: {
    inlineMath: [['$', '$'], ['\\(', '\\)']]
  },
  svg: {
    fontCache: 'global'
  }
};
</script>
<script type="text/javascript" id="MathJax-script" async
  src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-svg.js">
</script>
<style> body { font-family: "Roboto Mono", monospace; } </style>

<p align='center'><img src='https://64.media.tumblr.com/122cb8fcdabd68832c61b62a403bf49c/9eb1947e2ed393cf-ee/s540x810/06c37a959200146a91c2799c5175f6a9956276ae.jpg'></p>

<p>&nbsp; In Bayesian statistics, we are often interested in making an inference about data based on what we already have. Equivalently, it is the posterior distribution (which composes an uncertainty about yet-to-be observed variables) which is our topic of study. From Bayes' theorem, we set up the problem: </p>

$$\displaystyle p(z|x;\theta)=\frac{p(x|z;\theta)p(z;\theta)}{p(x;\theta)}$$

<p> Which just reinforces that the posterior is proportional to the likelihood times the prior. Note that $p(x;\theta)=\int p(x|z;\theta)p(z;\theta) \, dz$ is the evidence, which can bear a very high dimensionality (might be intractable). This is *no bueno* and is the source of many headaches, but also some cool algorithms. </p>

> <p>Variational inference seeks to give better approximations when our posterior density is not so tractable. </p>

<p>Let me make your life worse by presenting a set of local variational parameters $\phi_{i}$ which belong to $q(z|x_{i};\phi_{i})$. This pretty much says that the latent distribution of vector $z$ (given $i$ observations) is equipped by local parameters. Now, given that we have global parameters $\theta$, we could possibly update each $\phi_{i}$ upon each successive observation. As we update, we can get closer and closer to our global $\theta$. More on this later.</p>

<p>One of the central approaches to tackling this optimization problem is through the Kullback-Leibler (KL) divergence. Horribly informalized, it is the measure between our approximating distribution $q(z)$ and the true density $p(z)$. Now, we have the objective function:</p>

$$\displaystyle \mathcal{C}=\sum^{N}_{i=1}D_{KL}(q(z|x_{i};\phi_{i})\ ||\ p(z|x_{i};\theta))$$

<p>where $D_{KL}=\mathbb{E}_{q}[\log q(z|x_{i};\phi_{i})-\log p(z|x_{i};\theta)]$</p>
<br>
<p>Which is just the expectation w.r.t. $q$ of the difference between the log densities.
However, taking the expectations of a forward $D_{KL}$  does not yield a closed form. So we turn to approximations. Now, with a little bit of algebra, observe the following: </p>

$$\displaystyle 
\begin{align} 
\\
\mathcal{C}=\sum^{N}_{i=1} \mathbb{E}_{q}\left[\log q(z|x_{i};\phi_{i})-\log p(z|x_{i};\theta)\right] 
\\
=\sum^{N}_{i=1}\mathbb{E}_{q}\left[\log q(z|x_{i};\phi_{i})-\log\frac{p(x_{i},z;\theta)}{p(x_{i};\theta)}\right]
\\
=\sum^{N}_{i=1}\mathbb{E}_{q}\left[\log q(z|x_{i};\phi_{i})-\log p(x_{i},z;\theta)]+\sum^{N}_{i=1}\mathbb{E}_{q}[\log p(x_{i};\theta)\right]
\\
\end{align}$$

<p>The mean field approximation assumes that our variational posterior is fully factorizable</p>

$$\displaystyle q(z_{1},\dots,z_{N})=\prod^{N}_{k=1}q(z_{k})$$

by partitioning elements of $z$ into disjoint groupings $z_{k}$.

![alttext](https://www.google.com/url?sa=i&url=https%3A%2F%2Fwww.enworld.org%2Fmedia%2Fpeanut-butter-jelly-time-banana-gif.95112%2F&psig=AOvVaw0E98xwjOWrSoERm9CayGkU&ust=1710053807707000&source=images&cd=vfe&opi=89978449&ved=0CBIQjRxqFwoTCOCkk4DN5oQDFQAAAAAdAAAAABAE)


