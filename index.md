---
layout: default
---

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

<div class="hero-intro">
 <canvas id="waveCanvas"></canvas>

  <div class='content'>
    <p class = "hero-text"></p>
  </div>
    <script>
        const canvas = document.getElementById('waveCanvas');
        const ctx = canvas.getContext('2d');
        
        // constants
        const Nx = 200;
        let L = 0;
        let dx = 0;
        let x = [];
        let baseline = 0;
        let c = 1;
        let dt = 0
        const Nt = 100000; 
        let t = 0;

        resizeCanvas();

        // arrays
        let u = new Array(Nx).fill(0);
        let u_new = new Array(Nx).fill(0);
        let u_old = new Array(Nx).fill(0);
               
        // initial params
        const params = {
            A: 1 + Math.random() * 5,
            f: 5 + Math.random() * 30,
            B: 20 + Math.random() * 120,
            C: Math.random(),
            D: Math.random() * 2,
            g: 1 + Math.random() * 10
        };

        let signalMode = "wave";
        let modeUntil = 0;

        const modes = ["sawtooth", "square", "triangle", "pulse"];

        function maybeSwitchMode() {
            if (t < modeUntil) return;

            signalMode = "wave";

            if (Math.random() < 0.005) {
                signalMode = modes[Math.floor(Math.random() * modes.length)];
                modeUntil = t + 120 + Math.floor(Math.random() * 90);
            } 
        }

        function signalValue(i) {
            const cycles = 8;
            const phase = ((i / Nx) * cycles + t * 0.03) % 1;
            const amp = 35;

            if (signalMode === "sawtooth") {
                return amp * (2 * phase - 1);
            }

            if (signalMode === "square") {
                return phase < 0.5 ? amp : -amp;
            }

            if (signalMode === "triangle") {
                return amp * (1 - 4 * Math.abs(phase - 0.5));
            }

            if (signalMode === "pulse") {
                return phase < 0.15 ? amp : -amp * 0.35;
            }

            return u[i];
        }

        function clamp(v, lo, hi) {
            return Math.max(lo, Math.min(hi, v));
        }

        // Initial displacement (asymmetric plucking)
        function gaussianDisplacement(x) {
            return (
                params.A * Math.sin(params.f * Math.PI * x / L) *
                Math.exp(-params.B * (x / L - params.C) ** 2)
                +
                params.D * Math.cos(params.g * Math.PI * x / L)
            );
        }

        for (let i = 0; i < Nx; i++) {
            u[i] = gaussianDisplacement(x[i]);
            u_old[i] = u[i];
        }

        // Time points where additional plucking occurs
        const pluckingTimes = [50, 150, 300, 600, 900, 1000, 2000, 2430, 2700, 7000];
        const pluckingIntensity = 1.05; // Multiplier for plucking intensity
        
        function draw() {
            ctx.clearRect(0, 0, L, canvas.getBoundingClientRect().height);   
        
            const savedTheme = localStorage.getItem("theme") || "dark";
            ctx.strokeStyle = document.body.classList.contains("dark-mode") || savedTheme === "dark"
                ? 'white' : 'black';
           
            ctx.lineWidth = 2;
            ctx.beginPath();
            ctx.moveTo(0, baseline - signalValue(0));
            
            const maxAmp = canvas.getBoundingClientRect().height * 0.35;

            ctx.moveTo(0, baseline - clamp(signalValue(0), -maxAmp, maxAmp));

            for (let i = 1; i < Nx; i++) {
                const y = baseline - clamp(signalValue(i), -maxAmp, maxAmp);
                ctx.lineTo(i * dx, y);
            }

            ctx.stroke();
        }

        window.drawWave = draw;
        
        function updateWave() {
            if (t % 300 === 0) {
                c = 0.5 + Math.random() * 2.5;
                dt = 0.5 * dx / c;
            }

            if (Math.random() < 0.009) {
                const center = Math.random();
                const strength = 0.5 + Math.random() * 1.2;
                const width = 80 + Math.random() * 200;

                for (let i = 0; i < Nx; i++) {
                    const xi = x[i] / L;

                    const kick = strength * Math.exp(-width * (xi - center) **2);
                    u[i] += kick;
                    u_old[i] -= kick * 0.8;
                }
            }

            for (let j = 1; j < Nx - 1; j++) {
                const damping = 0.9997;
                u_new[j] = damping * (2 * u[j] - u_old[j] + (c * dt / dx) ** 2 * (u[j + 1] - 2 * u[j] + u[j - 1])); 
            }
            
            u_new[0] = 0;
            u_new[Nx - 1] = 0;
            [u_old, u, u_new] = [u, u_new, u_old];
            t++;
        
            maybeSwitchMode();
            draw();
            
            if (t < Nt) {
                requestAnimationFrame(updateWave);
            } 
        }
        
        function resizeCanvas() {
            const rect = canvas.getBoundingClientRect();
            const dpr = window.devicePixelRatio || 1;

            canvas.width = rect.width * dpr;
            canvas.height = rect.height * dpr;

            ctx.setTransform(dpr, 0, 0, dpr, 0, 0);

            L = rect.width;
            dx = L / Nx;
            dt = 0.5 * dx / c;
            baseline = rect.height * 0.45;
            x = Array.from({ length: Nx }, (_, i) => i * dx);
        }

        resizeCanvas();
        window.addEventListener("resize", resizeCanvas);

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
    </div>
