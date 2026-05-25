## The Replay Buffer and Prioritzed Experience Replay
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

<p align='center'><img src='https://cdn2.hubspot.net/hubfs/4638968/blog/johnfootefaculty-1.png'></p>

<p align='center'><i>All those moments will be lost in time, like tears in rain.</i></p>

In training an RL agent, we accumulate a wide variety of experiences from which we can store those that
may contribute to its learning. However, not all experiences are created equally, for some rare ones could
potentially prove useful further down the line. This idea of being cautious with what we throw away is the central idea 
before *experience replay* --- where previous experiences are relived again. *Prioritzed experience
replay* (PER) further enhances this idea by accounting for the relative frequencies of these events. 

An experience, in the RL sense, is much like how you'd expect. It is simply an event that has occurred from being in some state 
and taking an action that takes us to another state. We can formalize an experience as a tuple $(s, a, s', r)$ where taking 
the action $a$ in state $s$ results in a new state $s'$ along with some signal $r$. Often, $r$ is our reward signal.
Given this definition, we ought to find a way to quantify which experiences are useful, could be useful, or not useful. 

Among the many criteria, an ideal one involves measuring how much an agent can learn by transitioning from its current state.
The temporal difference (TD) error is one such method.

>“We have a view of the world, we anticipate outcomes, and when the difference between expectation and reality is significant, we know we need to learn something from that.”

Let our transition model be defined as $p(s'\mid s, a)$ which is the probability of reaching state $s'$ given
that we took action $a$ in state $s$. Furthermore, let $r(s)$ be a reward function that maps states to real-valued rewards (good states lead to 
better rewards). To quantify just how "good" our current state and action are in the grand scheme of things, we need to consider
all possible states in a larger space. Suppose $\mathcal{S}$ is our state space (number of grids, road lanes, joint configurations).
