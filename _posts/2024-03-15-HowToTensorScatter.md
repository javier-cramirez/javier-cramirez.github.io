## Tensor.scatter_() for Dummies
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

<p>Utilizes parameters: `dim`, `index`, `src`, `reduce`</p>
<p>Perhaps one of my favorite explanations of PyTorch's very confusing function is this: "`Tensor.scatter_()` essentially uses the information from `index` to place `src` into our beloved `Tensor`".</p>
