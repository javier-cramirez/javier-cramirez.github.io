## Stealth Walking and Leaping for Quadrupeds II
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

<p align='center'><img src='https://cdna.artstation.com/p/assets/images/images/015/669/734/large/kemal-yaralioglu-screenshot-01.jpg?1549194488'></p>

>Hey

In the previous post, we setup the problem, designed a quadruped robot (named *Wally*), picked an RL algorithm fresh off the shelf and X.
Now, we'll start going over how *Wally* will actually learn and the reward signals necessary for walking. From there, we will lookahead and 
figure out how to transition from walking to quiet walking.

When it comes to quiet walking, a very interesting paper I read was [Learning Quiet Walking for a Small Home Robot](https://arxiv.org/pdf/2502.10983). 
Something of value here was the authors' use of curriculum learning to train the robot dog to walk in two different phases: noisy walking and quiet walking.

How will we minimize noise if we don't have a microphone hooked up to *Wally*? Well, we can first look at minimizing the impact of its foot as it walks.
This means penalizing the foot contact velocity so that it learns to take more careful steps. Now, of course, this will only be used in settings where 
it *has to* stealth walk. To learn this, we will need to setup different goals for *Wally* to learn and figure out which requires which navigation scheme.
