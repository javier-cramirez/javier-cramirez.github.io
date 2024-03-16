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

<p>This little function Utilizes parameters: `dim`, `index`, `src`, `reduce`.</p>
<br>
> <p>`Tensor.scatter_()` essentially uses the information from `index` to place `src` into our beloved `Tensor`.</p>

<p>Suppose we have the following code</p>
```python
  src = torch.arange(1, 11).reshape((2, 5))
``` 
<p>Our tensor looks like:</p>
```python
tensor([[ 1,  2,  3,  4,  5],
        [ 6,  7,  8,  9, 10]])
```
