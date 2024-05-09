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

<p align='center'>When thinking of partitioning data points into groups, we intuitively turn to clustering. A very classcal example is that of K-means.
Briefly, the algorithm seeks to minimize the Euclidean distance between points in each assigned cluster $C$. Of course, partitioning the data requires
that (1) the union of all clusters is equal to the data set and (2) none of these clusters overlap. </p>
