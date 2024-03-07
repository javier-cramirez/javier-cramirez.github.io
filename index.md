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

I'm a current first-year at Arizona State University studying math.
My current interests are stochastic processes and diffusion models. 
Hopefully I'll post some blogs soon... 
![Book logo](IMG_4777.JPG)

<p align="center"><u>Formula of the Month:</u></p>
<p align="center">
  The Lagrange basis function 
  <br>
  $$\displaystyle L_{i}(x)=\prod^{N}_{j=1,i\neq j}\frac{x-x_{j}}{x_{i}-x_{j}}$$
  <br>
  This bad boy follows from the following result:
  <br>
  Suppose we have  $math f:[a,b]\rightarrow\mathbb{R}$ and $x_{1} < \dots < x_{n} \in [a,b]$. Then, there exists a unique polynomial, $p(x)$, with degree no greater than $n-1$ that interpolates $f$ at points $x_{1},\dots , x_{n}$. This interpolating polynomial can be expressed as:
  <br>                                                                     $$\displaystyle p(x)=\sum^{N}_{j=1}f(x_{j})q_{j}(x)$$ 
  <br>
  Where $q_{j}(x)$ is the Lagrange basis function.
</p>



