
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Code & Beyond</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            background: #000;
            color: #e0e0e0;
            font-family: 'Courier New', monospace;
            overflow-x: hidden;
            position: relative;
        }

        .matrix-bg {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: 0;
            opacity: 0.15;
        }

        .container {
            max-width: 1400px;
            margin: 0 auto;
            padding: 40px 20px;
            position: relative;
            z-index: 1;
        }

        .glitch {
            font-size: 4.5rem;
            font-weight: 900;
            text-align: center;
            color: #e50914;
            text-transform: uppercase;
            position: relative;
            letter-spacing: 8px;
            margin-bottom: 10px;
            animation: glitch 3s infinite;
        }

        .glitch::before,
        .glitch::after {
            content: attr(data-text);
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
        }

        .glitch::before {
            animation: glitch-1 0.3s infinite;
            color: #0ff;
            z-index: -1;
        }

        .glitch::after {
            animation: glitch-2 0.3s infinite;
            color: #ff00ff;
            z-index: -2;
        }

        @keyframes glitch {
            0%, 100% { transform: translate(0); }
            20% { transform: translate(-2px, 2px); }
            40% { transform: translate(-2px, -2px); }
            60% { transform: translate(2px, 2px); }
            80% { transform: translate(2px, -2px); }
        }

        @keyframes glitch-1 {
            0% { clip-path: inset(40% 0 61% 0); transform: translate(-2px, -2px); }
            20% { clip-path: inset(92% 0 1% 0); transform: translate(2px, 2px); }
            40% { clip-path: inset(43% 0 1% 0); transform: translate(-2px, 2px); }
            60% { clip-path: inset(25% 0 58% 0); transform: translate(2px, -2px); }
            80% { clip-path: inset(54% 0 7% 0); transform: translate(-2px, -2px); }
            100% { clip-path: inset(58% 0 43% 0); transform: translate(0); }
        }

        @keyframes glitch-2 {
            0% { clip-path: inset(67% 0 10% 0); transform: translate(2px, 2px); }
            20% { clip-path: inset(8% 0 50% 0); transform: translate(-2px, -2px); }
            40% { clip-path: inset(90% 0 5% 0); transform: translate(2px, -2px); }
            60% { clip-path: inset(32% 0 40% 0); transform: translate(-2px, 2px); }
            80% { clip-path: inset(75% 0 15% 0); transform: translate(2px, 2px); }
            100% { clip-path: inset(20% 0 65% 0); transform: translate(0); }
        }

        .header {
            text-align: center;
            margin-bottom: 60px;
        }

        .typing-container {
            min-height: 50px;
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 1.4rem;
            color: #e50914;
            margin: 20px 0;
        }

        .typing-text {
            font-style: italic;
            text-shadow: 0 0 10px rgba(229, 9, 20, 0.5);
        }

        .cursor {
            display: inline-block;
            width: 3px;
            height: 1.4rem;
            background: #e50914;
            margin-left: 4px;
            animation: blink 0.7s infinite;
        }

        @keyframes blink {
            0%, 50% { opacity: 1; }
            51%, 100% { opacity: 0; }
        }

        .terminal {
            background: rgba(10, 10, 10, 0.9);
            border: 2px solid #e50914;
            border-radius: 12px;
            padding: 30px;
            margin: 40px 0;
            box-shadow: 0 0 30px rgba(229, 9, 20, 0.3), inset 0 0 50px rgba(0, 0, 0, 0.5);
            position: relative;
            overflow: hidden;
        }

        .terminal::before {
            content: '';
            position: absolute;
            top: -2px;
            left: -2px;
            right: -2px;
            bottom: -2px;
            background: linear-gradient(45deg, #e50914, #1a237e, #e50914);
            z-index: -1;
            filter: blur(10px);
            opacity: 0.7;
            animation: rotate 3s linear infinite;
        }

        @keyframes rotate {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }

        .terminal-header {
            display: flex;
            align-items: center;
            margin-bottom: 20px;
            padding-bottom: 15px;
            border-bottom: 1px solid #333;
        }

        .terminal-button {
            width: 12px;
            height: 12px;
            border-radius: 50%;
            margin-right: 8px;
        }

        .btn-red { background: #ff5f56; }
        .btn-yellow { background: #ffbd2e; }
        .btn-green { background: #27c93f; }

        .terminal-title {
            margin-left: 15px;
            color: #666;
            font-size: 0.9rem;
        }

        .code-line {
            margin: 8px 0;
            opacity: 0;
            animation: fadeInLine 0.5s forwards;
        }

        .code-line:nth-child(1) { animation-delay: 0.1s; }
        .code-line:nth-child(2) { animation-delay: 0.2s; }
        .code-line:nth-child(3) { animation-delay: 0.3s; }
        .code-line:nth-child(4) { animation-delay: 0.4s; }
        .code-line:nth-child(5) { animation-delay: 0.5s; }
        .code-line:nth-child(6) { animation-delay: 0.6s; }
        .code-line:nth-child(7) { animation-delay: 0.7s; }
        .code-line:nth-child(8) { animation-delay: 0.8s; }

        @keyframes fadeInLine {
            from { opacity: 0; transform: translateX(-20px); }
            to { opacity: 1; transform: translateX(0); }
        }

        .keyword { color: #ff79c6; }
        .function { color: #50fa7b; }
        .string { color: #f1fa8c; }
        .comment { color: #6272a4; }
        .number { color: #bd93f9; }

        .skills-matrix {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 30px;
            margin: 50px 0;
        }

        .skill-cube {
            background: rgba(10, 10, 10, 0.8);
            border: 1px solid #1a237e;
            border-radius: 10px;
            padding: 30px;
            position: relative;
            transition: all 0.4s ease;
            cursor: pointer;
        }

        .skill-cube::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: linear-gradient(135deg, rgba(229, 9, 20, 0.1), rgba(26, 35, 126, 0.1));
            opacity: 0;
            transition: 0.4s;
            border-radius: 10px;
        }

        .skill-cube:hover::before {
            opacity: 1;
        }

        .skill-cube:hover {
            transform: translateY(-10px) scale(1.02);
            border-color: #e50914;
            box-shadow: 0 15px 40px rgba(229, 9, 20, 0.4);
        }

        .skill-icon {
            font-size: 3rem;
            margin-bottom: 15px;
            display: block;
            filter: drop-shadow(0 0 10px rgba(229, 9, 20, 0.5));
        }

        .skill-name {
            font-size: 1.6rem;
            font-weight: 700;
            color: #e50914;
            margin-bottom: 10px;
        }

        .skill-projects {
            color: #888;
            font-size: 1rem;
            margin-bottom: 15px;
        }

        .skill-bar-container {
            width: 100%;
            height: 10px;
            background: #1a1a1a;
            border-radius: 5px;
            overflow: hidden;
            margin-top: 15px;
            position: relative;
        }

        .skill-bar {
            height: 100%;
            background: linear-gradient(90deg, #e50914, #1a237e);
            border-radius: 5px;
            position: relative;
            animation: skillLoad 2s ease-out forwards;
            transform-origin: left;
            box-shadow: 0 0 10px rgba(229, 9, 20, 0.6);
        }

        @keyframes skillLoad {
            from { transform: scaleX(0); }
            to { transform: scaleX(1); }
        }

        .pulse-dot {
            width: 8px;
            height: 8px;
            background: #e50914;
            border-radius: 50%;
            position: absolute;
            top: 50%;
            right: 5px;
            transform: translateY(-50%);
            animation: pulse 2s infinite;
        }

        @keyframes pulse {
            0%, 100% { box-shadow: 0 0 0 0 rgba(229, 9, 20, 0.7); }
            50% { box-shadow: 0 0 0 10px rgba(229, 9, 20, 0); }
        }

        .particles {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 0;
        }

        .particle {
            position: absolute;
            width: 4px;
            height: 4px;
            background: #e50914;
            border-radius: 50%;
            animation: float 4s infinite;
            opacity: 0.6;
        }

        @keyframes float {
            0% { transform: translateY(100vh) scale(0); opacity: 0; }
            10% { opacity: 0.6; }
            90% { opacity: 0.6; }
            100% { transform: translateY(-100vh) scale(1); opacity: 0; }
        }

        .stats-panel {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 25px;
            margin: 50px 0;
        }

        .stat-card {
            background: rgba(10, 10, 10, 0.9);
            border: 2px solid #1a237e;
            border-radius: 10px;
            padding: 30px;
            text-align: center;
            position: relative;
            overflow: hidden;
            transition: all 0.3s ease;
        }

        .stat-card::before {
            content: '';
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: linear-gradient(45deg, transparent, rgba(229, 9, 20, 0.1), transparent);
            animation: scan 3s linear infinite;
        }

        @keyframes scan {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }

        .stat-card:hover {
            border-color: #e50914;
            transform: scale(1.05);
            box-shadow: 0 10px 30px rgba(229, 9, 20, 0.3);
        }

        .stat-value {
            font-size: 3rem;
            font-weight: 900;
            color: #e50914;
            text-shadow: 0 0 20px rgba(229, 9, 20, 0.8);
            position: relative;
            z-index: 1;
        }

        .stat-label {
            color: #888;
            text-transform: uppercase;
            letter-spacing: 2px;
            font-size: 0.9rem;
            margin-top: 10px;
            position: relative;
            z-index: 1;
        }

        .footer {
            text-align: center;
            margin-top: 80px;
            padding: 30px;
            border-top: 1px solid #1a237e;
            color: #666;
            font-size: 1.1rem;
        }

        .binary-rain {
            position: absolute;
            font-size: 14px;
            color: #e50914;
            opacity: 0.3;
            animation: fall linear infinite;
        }

        @keyframes fall {
            to { transform: translateY(100vh); }
        }
    </style>
</head>
<body>
    <canvas class="matrix-bg" id="matrixCanvas"></canvas>
    <div class="particles" id="particles"></div>

    <div class="container">
        <div class="header">
            <h1 class="glitch" data-text="CODE & BEYOND">CODE & BEYOND</h1>
            <div class="typing-container">
                <span class="typing-text" id="typingText"></span>
                <span class="cursor"></span>
            </div>
        </div>

        <div class="stats-panel">
            <div class="stat-card">
                <div class="stat-value" id="statProjects">0</div>
                <div class="stat-label">Total Projects</div>
            </div>
            <div class="stat-card">
                <div class="stat-value" id="statLanguages">0</div>
                <div class="stat-label">Languages Mastered</div>
            </div>
            <div class="stat-card">
                <div class="stat-value" id="statCommits">0</div>
                <div class="stat-label">Commits Made</div>
            </div>
            <div class="stat-card">
                <div class="stat-value" id="statHours">0</div>
                <div class="stat-label">Hours Coded</div>
            </div>
        </div>

        <div class="terminal">
            <div class="terminal-header">
                <div class="terminal-button btn-red"></div>
                <div class="terminal-button btn-yellow"></div>
                <div class="terminal-button btn-green"></div>
                <div class="terminal-title">~/portfolio/tech_stack.py</div>
            </div>
            <div class="terminal-body">
                <div class="code-line"><span class="keyword">class</span> <span class="function">Developer</span>:</div>
                <div class="code-line">    <span class="keyword">def</span> <span class="function">__init__</span>(self):</div>
                <div class="code-line">        self.languages = [<span class="string">"Python"</span>, <span class="string">"JavaScript"</span>, <span class="string">"Java"</span>, <span class="string">"SQL"</span>]</div>
                <div class="code-line">        self.frameworks = [<span class="string">"React"</span>, <span class="string">"TensorFlow"</span>]</div>
                <div class="code-line">        self.skills = [<span class="string">"Machine Learning"</span>, <span class="string">"Web Dev"</span>, <span class="string">"CSS"</span>]</div>
                <div class="code-line">        self.motto = <span class="string">"CODE IS ART"</span></div>
                <div class="code-line">    </div>
                <div class="code-line"><span class="comment"># Building the future, one algorithm at a time...</span></div>
            </div>
        </div>

        <div class="skills-matrix" id="skillsMatrix"></div>

        <div class="footer">
            <p>⚡ Powered by Passion | 🎯 Driven by Innovation | 💻 Crafted with Code</p>
        </div>
    </div>

    <script>
        const skills = [
            { name: 'Python', icon: '🐍', projects: 24, level: 95 },
            { name: 'JavaScript', icon: '⚡', projects: 18, level: 90 },
            { name: 'Java', icon: '☕', projects: 15, level: 85 },
            { name: 'React', icon: '⚛️', projects: 12, level: 88 },
            { name: 'SQL', icon: '🗄️', projects: 20, level: 82 },
            { name: 'CSS', icon: '🎨', projects: 22, level: 87 },
            { name: 'Machine Learning', icon: '🤖', projects: 10, level: 80 }
        ];

        const phrases = [
            "where code becomes art...",
            "transforming logic into innovation...",
            "building digital masterpieces...",
            "crafting intelligent solutions...",
            "engineering the impossible..."
        ];

        let phraseIndex = 0;
        let charIndex = 0;
        let isDeleting = false;

        function typeWriter() {
            const current = phrases[phraseIndex];
            const element = document.getElementById('typingText');
            
            if (isDeleting) {
                element.textContent = current.substring(0, charIndex - 1);
                charIndex--;
            } else {
                element.textContent = current.substring(0, charIndex + 1);
                charIndex++;
            }

            let speed = isDeleting ? 50 : 100;

            if (!isDeleting && charIndex === current.length) {
                speed = 2000;
                isDeleting = true;
            } else if (isDeleting && charIndex === 0) {
                isDeleting = false;
                phraseIndex = (phraseIndex + 1) % phrases.length;
                speed = 500;
            }

            setTimeout(typeWriter, speed);
        }

        function renderSkills() {
            const container = document.getElementById('skillsMatrix');
            skills.forEach((skill, index) => {
                const card = document.createElement('div');
                card.className = 'skill-cube';
                card.style.animationDelay = `${index * 0.1}s`;
                card.innerHTML = `
                    <span class="skill-icon">${skill.icon}</span>
                    <div class="skill-name">${skill.name}</div>
                    <div class="skill-projects">${skill.projects} Projects Completed</div>
                    <div class="skill-bar-container">
                        <div class="skill-bar" style="width: ${skill.level}%">
                            <div class="pulse-dot"></div>
                        </div>
                    </div>
                `;
                container.appendChild(card);
            });
        }

        function animateStats() {
            const stats = [
                { id: 'statProjects', target: 121, suffix: '' },
                { id: 'statLanguages', target: 7, suffix: '+' },
                { id: 'statCommits', target: 2547, suffix: '+' },
                { id: 'statHours', target: 1340, suffix: '+' }
            ];

            stats.forEach(stat => {
                let current = 0;
                const increment = stat.target / 100;
                const timer = setInterval(() => {
                    current += increment;
                    if (current >= stat.target) {
                        document.getElementById(stat.id).textContent = stat.target + stat.suffix;
                        clearInterval(timer);
                    } else {
                        document.getElementById(stat.id).textContent = Math.floor(current) + stat.suffix;
                    }
                }, 20);
            });
        }

        // Matrix rain effect
        const matrixCanvas = document.getElementById('matrixCanvas');
        const ctx = matrixCanvas.getContext('2d');
        matrixCanvas.width = window.innerWidth;
        matrixCanvas.height = window.innerHeight;

        const chars = '01アイウエオカキクケコサシスセソタチツテトナニヌネノハヒフヘホマミムメモヤユヨラリルレロワヲン';
        const fontSize = 14;
        const columns = matrixCanvas.width / fontSize;
        const drops = Array(Math.floor(columns)).fill(1);

        function drawMatrix() {
            ctx.fillStyle = 'rgba(0, 0, 0, 0.05)';
            ctx.fillRect(0, 0, matrixCanvas.width, matrixCanvas.height);
            
            ctx.fillStyle = '#e50914';
            ctx.font = fontSize + 'px monospace';

            for (let i = 0; i < drops.length; i++) {
                const text = chars[Math.floor(Math.random() * chars.length)];
                ctx.fillText(text, i * fontSize, drops[i] * fontSize);

                if (drops[i] * fontSize > matrixCanvas.height && Math.random() > 0.975) {
                    drops[i] = 0;
                }
                drops[i]++;
            }
        }

        setInterval(drawMatrix, 35);

        // Floating particles
        function createParticles() {
            const container = document.getElementById('particles');
            for (let i = 0; i < 20; i++) {
                const particle = document.createElement('div');
                particle.className = 'particle';
                particle.style.left = Math.random() * 100 + '%';
                particle.style.animationDuration = (Math.random() * 3 + 2) + 's';
                particle.style.animationDelay = Math.random() * 5 + 's';
                container.appendChild(particle);
            }
        }

        window.addEventListener('resize', () => {
            matrixCanvas.width = window.innerWidth;
            matrixCanvas.height = window.innerHeight;
        });

        typeWriter();
        renderSkills();
        animateStats();
        createParticles();
    </script>
</body>
</html>
