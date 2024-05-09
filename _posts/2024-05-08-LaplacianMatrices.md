## Laplacians and Spectral Clustering

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

<p>When thinking of partitioning data points into groups, we intuitively turn to clustering. A very classcal example is that of K-means.
Briefly, the algorithm seeks to minimize the Euclidean distance between points in each assigned cluster $C$. Of course, partitioning the data requires
that (1) the union of all clusters is equal to the data set and (2) none of these clusters overlap. </p>
<br>
<p>The algorithm is very often associated with Lloyd's algorithm. Select a set of $n$ distinct points from some domain $\phi$. Assign each point to the closest cluster mean $c_{i}$ and repeat. Very informally, of course. However, these traditional methods are limited to spherical clusters, leading to worse performance on more unusual cluster shapes. As it turns out, spectral clustering is a very nice method leveraging the eigenvalues and eigenvectors of a special structure called the similarity matrix. For this, we must turn to principles from graph theory. </p>
<br>
<p>Define the graph $G=(V,E)$ where $E\subseteq \binom{V}{2}$ where $E$ is a set of edges and $V$ is a set of vertices. $\binom{V}{2}$ is the set of all 2-element subsets of $V$ given that $V$ is finite. We say that $u\in V$ and $v\in V$ are adjacent if $\{u,v\}\in E$. This works both ways, which also means $\{v,u\}\in E$. To define the degree of a graph, first note that the neighborhood $N(V)$ of $V$ for $v\in V$ is the set of all vertices adjacent to $v$. Thus, the cardinality of $N(V)=\text{deg}(v)$. The adjacency matrix, $\mathbf{A}$, has its $(i,j)$-th entry set to $1$ if $v_{i}$ is adjacent to $v_{j}$ and $0$ otherwise. Next, define the incidence matrix, $\mathbf{M}$, as having its $(i,j)$-th entry set to $1$ is $v_{i}\in e{j}$ and $0$ otherwise. Generally, if $v\in e$, then we say that $v$ is incident with $e$ and vice versa. </p>

<p>Further note that $\sum^{n}_{j=1}A(i,j)=\text{deg}(v_{i})=\sum^{n}_{j=1}A(j,i)$. Now, define the matrix $\mathbf{D}$ as the matrix whose diagonal elements $\mathbf{D}(i,i)$ to be $\text{deg}(v_{i})$. We define the unnormalized Laplacian as $\mathbf{L}=\mathbf{D}-\mathbf{A}$. Notable properties of $L$ is that (1) its smallest eigenvalue, $\lambda_{1} is $0$, with a constant eigenvector $\mathbb{1}$, (2) the multiplicity of $\lambda_{1}$ is equal to the number of components of $G$, and (3) it has $n$ non-negative real-valued eigenvalues in increasing order. Did I mention $\mathbf{L}$ is positive semi-definite and symmetric?</p>
