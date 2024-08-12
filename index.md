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
<style> 
  body, html { 
    font-family: "Roboto Mono", monospace;
    margin: 0;
    padding: 0;
  } 
  #waveCanvas {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    z-index: -1;
  }
  .content {
    position: relative;
    z-index: 1;
    color: black;
    opacity: 1.0;
  }
  .pacman-background {
    background-image: url("https://cdn.vox-cdn.com/uploads/chorus_asset/file/19992985/pac_man_gamegan_320.gif");
    background-size: cover;
    background-position: center;
  } 
  .visible {
    opacity: 1.0;
  }
  .invisible {
    opacity: 0.0;
  }
  .pacman-time {
    text-decoration: none;
    color: yellow; 
    opacity: 0.0;
  }
</style>


<body>
 <canvas id="waveCanvas" width="800" height="400"></canvas>
  <div class='content'>
    <p class = "normal-time">Current sophomore at Arizona State University. Interested in intelligent systems.</p>
    <p class = "pacman-time">Sometimes games as well.</p>
  </div>
    <script>
        const canvas = document.getElementById('waveCanvas');
        const ctx = canvas.getContext('2d');
        const L = canvas.width;
        const Nx = 200;
        const dx = L / Nx;
        const c = 1;
        const dt = 0.5 * dx / c;
        const Nt = 100000;
        let t = 0;
        const x = Array.from({ length: Nx }, (_, i) => i * dx);
        let u = new Array(Nx).fill(0);
        let u_new = new Array(Nx).fill(0);
        let u_old = new Array(Nx).fill(0);
        // Initial displacement (asymmetric plucking)
        function initialDisplacement(x) {
            const A = 3.0;
            const f = 20;
            const B = 100;
            const C = 0.3;
            const D = 1.0;
            const g = 5;
            return A * Math.sin(f * Math.PI * x / L) * Math.exp(-B * (x / L - C) ** 2) + D * Math.cos(g * Math.PI * x / L);
        }
        // Set initial conditions
        for (let i = 0; i < Nx; i++) {
            u[i] = initialDisplacement(x[i]);
            u_old[i] = u[i];
        }
        // Time points where additional plucking occurs
        const pluckingTimes = [50, 150, 300, 600, 900, 1000, 2000, 2430, 2700, 7000];
        const pluckingIntensity = 1.1; // Multiplier for plucking intensity
        function draw() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            ctx.beginPath();
            ctx.moveTo(0, canvas.height / 2 - u[0]);
            for (let i = 1; i < Nx; i++) {
                ctx.lineTo(i * dx, canvas.height / 2 - u[i]);
            }
            ctx.stroke();
        }
        function updateWave() {
            if (pluckingTimes.includes(t)) {
                for (let i = 0; i < Nx; i++) {
                    u[i] += pluckingIntensity * initialDisplacement(x[i]);
                }
            }
            for (let j = 1; j < Nx - 1; j++) {
                u_new[j] = 2 * u[j] - u_old[j] + (c * dt / dx) ** 2 * (u[j + 1] - 2 * u[j] + u[j - 1]);
            }
            [u_old, u, u_new] = [u, u_new, u_old];
            t++;
            draw();
            if (t < Nt) {
                requestAnimationFrame(updateWave);
            }
        }
        draw();
        requestAnimationFrame(updateWave);
        const pacmanText = document.querySelectorAll(".pacman-time");
        const content = document.querySelectorAll('.normal-time');
        content.forEach(link => {
            link.addEventListener('mouseenter', () => {
                canvas.classList.add('pacman-background');
                pacmanText.classList.add('visible');
                content.classList.add('invisible');
            });
            link.addEventListener('mouseleave', () => {
                canvas.classList.remove('pacman-background');
                pacmanText.classList.remove('visible');
                content.classList.remove('invisible');
            });
        });
        
    </script>
    </body>

  



