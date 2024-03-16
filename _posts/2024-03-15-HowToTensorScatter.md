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
> <p>`Tensor.scatter_()` essentially uses the information from `index` to place `src` into our beloved `Tensor`.</p>

<p>Suppose we have the following code: 
```python
  src = torch.arange(1, 11).reshape((2, 5))
``` Our tensor looks like this: 
```python
tensor([[ 1,  2,  3,  4,  5],
        [ 6,  7,  8,  9, 10]])
```
</p>
