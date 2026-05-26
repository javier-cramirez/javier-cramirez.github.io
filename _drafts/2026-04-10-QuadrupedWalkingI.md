## Stealth Walking and Leaping for Quadrupeds I
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
<p align='center'><img src='https://explorewithalec.com/wp-content/uploads/2025/06/mount-dickerman-hike-861A1108-scaled.jpg'></p>

>Ever wondered how the Leaper from *Arc Raiders* was trained? Everytime I encounter the four-legged gargantuan, I start to wonder how *Embark Studios*
pulled it off. I mean, a couple vague blog posts about the "power of reinforcement learning" just didn't satisfy me! It shouldn't satisfy you
either! As such, all of this came about because I got mad a proprietary studio did not give... well... their proprietary secrets.



Most papers deal with *sim-to-real* training methods as they usually deal with real robots (you know, the primary motivation for their research in the first place).
Given that I know nothing about robotics and am not actually designed a real life *Wally*, we have to do just purely simulation training.



However, transferring this XML design to a URDF format for IsaacSim proved a little lengthy for me. 
