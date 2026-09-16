<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Lucas Matheus | Dev Profile</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        :root {
            --primary: #00ff88;
            --secondary: #ff006e;
            --tertiary: #00d9ff;
            --dark-bg: #0a0e27;
            --card-bg: #1a1f3a;
            --text-primary: #e0e0e0;
            --text-secondary: #b0b0b0;
            --accent: #ff00ff;
        }

        body {
            font-family: 'Courier New', monospace;
            background: linear-gradient(135deg, #0a0e27 0%, #1a1f3a 50%, #0a0e27 100%);
            background-attachment: fixed;
            color: var(--text-primary);
            line-height: 1.6;
            overflow-x: hidden;
        }

        /* Animated Background */
        body::before {
            content: '';
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: 
                repeating-linear-gradient(
                    0deg,
                    rgba(0, 255, 136, 0.02) 0px,
                    rgba(0, 255, 136, 0.02) 1px,
                    transparent 1px,
                    transparent 2px
                );
            pointer-events: none;
            animation: scanlines 8s linear infinite;
            z-index: -1;
        }

        @keyframes scanlines {
            0% { transform: translateY(0); }
            100% { transform: translateY(10px); }
        }

        .container {
            max-width: 1000px;
            margin: 0 auto;
            padding: 40px 20px;
            position: relative;
            z-index: 1;
        }

        /* Header */
        .header {
            text-align: center;
            margin-bottom: 60px;
            position: relative;
        }

        .glitch {
            position: relative;
            display: inline-block;
            font-size: 4rem;
            font-weight: bold;
            text-transform: uppercase;
            letter-spacing: 8px;
            background: linear-gradient(45deg, #00ff88, #00d9ff, #ff006e);
            background-size: 300% 300%;
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            animation: gradient-shift 3s ease infinite, glitch-anim 0.3s cubic-bezier(0.25, 0.46, 0.45, 0.94) infinite;
        }

        @keyframes gradient-shift {
            0% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
            100% { background-position: 0% 50%; }
        }

        @keyframes glitch-anim {
            0% { text-shadow: -2px 0 #ff006e, 2px 0 #00d9ff; }
            50% { text-shadow: -2px 0 #00d9ff, 2px 0 #ff006e; }
            100% { text-shadow: -2px 0 #ff006e, 2px 0 #00d9ff; }
        }

        .typing-text {
            font-size: 1.2rem;
            margin-top: 20px;
            color: var(--primary);
            min-height: 30px;
            position: relative;
        }

        .typing-text::after {
            content: '█';
            animation: blink 0.7s infinite;
            margin-left: 4px;
        }

        @keyframes blink {
            0%, 50% { opacity: 1; }
            51%, 100% { opacity: 0; }
        }

        /* Terminal Box */
        .terminal-box {
            background: var(--card-bg);
            border: 2px solid var(--primary);
            border-radius: 8px;
            padding: 30px;
            margin-bottom: 40px;
            position: relative;
            overflow: hidden;
            box-shadow: 0 0 20px rgba(0, 255, 136, 0.2);
            animation: terminal-glow 3s ease-in-out infinite;
        }

        @keyframes terminal-glow {
            0%, 100% { box-shadow: 0 0 20px rgba(0, 255, 136, 0.2), inset 0 0 20px rgba(0, 255, 136, 0.05); }
            50% { box-shadow: 0 0 30px rgba(0, 255, 136, 0.4), inset 0 0 30px rgba(0, 255, 136, 0.1); }
        }

        .terminal-header {
            display: flex;
            gap: 8px;
            margin-bottom: 20px;
            align-items: center;
        }

        .dot {
            width: 12px;
            height: 12px;
            border-radius: 50%;
            animation: pulse 2s ease-in-out infinite;
        }

        .dot:nth-child(1) { background: #ff006e; animation-delay: 0s; }
        .dot:nth-child(2) { background: #ffbe0b; animation-delay: 0.2s; }
        .dot:nth-child(3) { background: #00ff88; animation-delay: 0.4s; }

        @keyframes pulse {
            0%, 100% { opacity: 1; transform: scale(1); }
            50% { opacity: 0.6; transform: scale(1.1); }
        }

        .terminal-header span {
            font-size: 0.9rem;
            color: var(--text-secondary);
            margin-left: 10px;
        }

        .terminal-line {
            margin: 10px 0;
            animation: fadeInUp 0.6s ease-out forwards;
            opacity: 0;
        }

        @keyframes fadeInUp {
            from {
                opacity: 0;
                transform: translateY(10px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .command {
            color: var(--primary);
            font-weight: bold;
        }

        .output {
            color: var(--tertiary);
            margin-left: 20px;
        }

        /* Sections */
        .section {
            margin-bottom: 50px;
        }

        .section-title {
            font-size: 2rem;
            margin-bottom: 30px;
            position: relative;
            display: inline-block;
            padding-bottom: 10px;
            color: var(--secondary);
            text-transform: uppercase;
            letter-spacing: 4px;
        }

        .section-title::after {
            content: '';
            position: absolute;
            bottom: 0;
            left: 0;
            width: 0;
            height: 2px;
            background: linear-gradient(90deg, var(--primary), var(--tertiary), var(--secondary));
            animation: expandWidth 0.8s ease-out forwards;
        }

        @keyframes expandWidth {
            to { width: 100%; }
        }

        /* Grid Layout */
        .grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            margin-bottom: 30px;
        }

        .card {
            background: linear-gradient(135deg, rgba(0, 255, 136, 0.1), rgba(0, 217, 255, 0.1));
            border: 1px solid var(--primary);
            border-radius: 8px;
            padding: 20px;
            position: relative;
            overflow: hidden;
            transition: all 0.3s ease;
            cursor: pointer;
        }

        .card::before {
            content: '';
            position: absolute;
            top: -50%;
            right: -50%;
            width: 100%;
            height: 100%;
            background: linear-gradient(45deg, transparent, rgba(255, 255, 255, 0.1), transparent);
            animation: shine 3s infinite;
            pointer-events: none;
        }

        @keyframes shine {
            0% { transform: translate(-100%, -100%) rotate(45deg); }
            100% { transform: translate(100%, 100%) rotate(45deg); }
        }

        .card:hover {
            background: linear-gradient(135deg, rgba(0, 255, 136, 0.2), rgba(0, 217, 255, 0.2));
            box-shadow: 0 0 20px rgba(0, 255, 136, 0.3);
            transform: translateY(-5px);
            border-color: var(--tertiary);
        }

        .card-title {
            font-size: 1.3rem;
            color: var(--tertiary);
            margin-bottom: 15px;
            font-weight: bold;
            text-transform: uppercase;
            letter-spacing: 2px;
        }

        .card-content {
            font-size: 0.95rem;
            color: var(--text-secondary);
            line-height: 1.8;
        }

        /* Badges */
        .badges {
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
            margin: 30px 0;
        }

        .badge {
            display: inline-block;
            background: linear-gradient(135deg, rgba(0, 255, 136, 0.15), rgba(0, 217, 255, 0.15));
            border: 1px solid var(--primary);
            padding: 8px 16px;
            border-radius: 20px;
            font-size: 0.85rem;
            color: var(--primary);
            transition: all 0.3s ease;
            text-transform: uppercase;
            letter-spacing: 1px;
            animation: float 3s ease-in-out infinite;
        }

        @keyframes float {
            0%, 100% { transform: translateY(0px); }
            50% { transform: translateY(-5px); }
        }

        .badge:hover {
            background: linear-gradient(135deg, rgba(255, 0, 110, 0.2), rgba(0, 217, 255, 0.2));
            border-color: var(--secondary);
            color: var(--secondary);
            box-shadow: 0 0 15px rgba(255, 0, 110, 0.3);
        }

        .badge:nth-child(even) {
            border-color: var(--tertiary);
            color: var(--tertiary);
            animation-delay: 0.5s;
        }

        .badge:nth-child(3n) {
            border-color: var(--secondary);
            color: var(--secondary);
            animation-delay: 1s;
        }

        /* Stack Section */
        .stack-group {
            margin-bottom: 40px;
        }

        .stack-label {
            color: var(--tertiary);
            font-size: 1.1rem;
            font-weight: bold;
            margin-bottom: 15px;
            text-transform: uppercase;
            letter-spacing: 2px;
        }

        /* Process Flow */
        .process-flow {
            display: flex;
            justify-content: space-around;
            align-items: center;
            margin: 50px 0;
            position: relative;
            flex-wrap: wrap;
            gap: 20px;
        }

        .process-step {
            text-align: center;
            flex: 1;
            min-width: 120px;
            position: relative;
        }

        .step-circle {
            width: 80px;
            height: 80px;
            margin: 0 auto 15px;
            border-radius: 50%;
            background: linear-gradient(135deg, var(--primary), var(--tertiary));
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 2rem;
            font-weight: bold;
            color: var(--dark-bg);
            position: relative;
            animation: rotateBorder 3s linear infinite;
            box-shadow: 0 0 20px rgba(0, 255, 136, 0.4);
        }

        @keyframes rotateBorder {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }

        .step-circle::after {
            content: '';
            position: absolute;
            inset: -2px;
            border-radius: 50%;
            border: 2px solid var(--primary);
            opacity: 0.5;
        }

        .step-title {
            color: var(--text-primary);
            font-weight: bold;
            font-size: 1rem;
            text-transform: uppercase;
        }

        .process-arrow {
            display: none;
            color: var(--primary);
            font-size: 2rem;
            animation: slideRight 1.5s ease-in-out infinite;
        }

        @media (min-width: 768px) {
            .process-arrow {
                display: block;
            }
        }

        @keyframes slideRight {
            0% { transform: translateX(-10px); opacity: 0.5; }
            50% { transform: translateX(0px); opacity: 1; }
            100% { transform: translateX(-10px); opacity: 0.5; }
        }

        /* Footer */
        .footer {
            text-align: center;
            margin-top: 80px;
            padding-top: 40px;
            border-top: 2px solid var(--primary);
            position: relative;
        }

        .social-links {
            display: flex;
            justify-content: center;
            gap: 20px;
            margin-bottom: 30px;
        }

        .social-link {
            display: inline-flex;
            align-items: center;
            gap: 8px;
            padding: 12px 24px;
            background: linear-gradient(135deg, rgba(0, 255, 136, 0.2), rgba(0, 217, 255, 0.2));
            border: 1px solid var(--primary);
            border-radius: 30px;
            color: var(--text-primary);
            text-decoration: none;
            transition: all 0.3s ease;
            font-weight: bold;
            text-transform: uppercase;
            letter-spacing: 1px;
            cursor: pointer;
        }

        .social-link:hover {
            background: linear-gradient(135deg, rgba(0, 255, 136, 0.4), rgba(0, 217, 255, 0.4));
            box-shadow: 0 0 30px rgba(0, 255, 136, 0.5);
            transform: scale(1.05);
        }

        .quote {
            font-size: 1.1rem;
            color: var(--tertiary);
            font-style: italic;
            margin-top: 30px;
            animation: fadeInDown 1s ease-out forwards;
        }

        @keyframes fadeInDown {
            from {
                opacity: 0;
                transform: translateY(-20px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        /* Responsive */
        @media (max-width: 768px) {
            .glitch {
                font-size: 2.5rem;
                letter-spacing: 4px;
            }

            .section-title {
                font-size: 1.5rem;
            }

            .process-flow {
                flex-direction: column;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- Header -->
        <div class="header">
            <div class="glitch">LUCAS MATHEUS</div>
            <div class="typing-text" id="typingText"></div>
        </div>

        <!-- Terminal Box -->
        <div class="terminal-box">
            <div class="terminal-header">
                <div class="dot"></div>
                <div class="dot"></div>
                <div class="dot"></div>
                <span>lucas@dev:~$</span>
            </div>
            <div class="terminal-line" style="animation-delay: 0s;">
                <span class="command">$ whoami</span>
            </div>
            <div class="terminal-line" style="animation-delay: 0.1s;">
                <span class="output">Software Developer | Linux Enthusiast | Security Explorer</span>
            </div>
            <div class="terminal-line" style="animation-delay: 0.2s;">
                <span class="command">$ cat interests.txt</span>
            </div>
            <div class="terminal-line" style="animation-delay: 0.3s;">
                <span class="output">Backend Development, Linux Systems, Cybersecurity, Open Source</span>
            </div>
            <div class="terminal-line" style="animation-delay: 0.4s;">
                <span class="command">$ echo $status</span>
            </div>
            <div class="terminal-line" style="animation-delay: 0.5s;">
                <span class="output">ONLINE & BUILDING</span>
            </div>
        </div>

        <!-- About Section -->
        <div class="section">
            <h2 class="section-title">About Me</h2>
            <p style="margin-top: 30px; font-size: 1.05rem;">
                Estudante de <strong>Análise e Desenvolvimento de Sistemas (ADS) no IFSP</strong>, construindo meu caminho através do desenvolvimento de software com foco profundo em entender como os sistemas funcionam em cada camada.
            </p>
            <p style="margin-top: 20px;">
                Apaixonado por <strong>backend development</strong>, ambientes <strong>Linux</strong>, <strong>cybersecurity</strong> e o ecossistema <strong>open source</strong>. Prefiro entender a tecnologia em profundidade—da arquitetura de aplicações até os internals do sistema operacional.
            </p>
        </div>

        <!-- Tech Stack -->
        <div class="section">
            <h2 class="section-title">Tech Stack</h2>
            
            <div class="stack-group">
                <div class="stack-label">Languages</div>
                <div class="badges">
                    <span class="badge">Python</span>
                    <span class="badge">C</span>
                    <span class="badge">C++</span>
                    <span class="badge">Java</span>
                    <span class="badge">TypeScript</span>
                    <span class="badge">JavaScript</span>
                </div>
            </div>

            <div class="stack-group">
                <div class="stack-label">Web & Frontend</div>
                <div class="badges">
                    <span class="badge">Angular</span>
                    <span class="badge">HTML5</span>
                    <span class="badge">CSS3</span>
                    <span class="badge">React</span>
                </div>
            </div>

            <div class="stack-group">
                <div class="stack-label">Databases & Backend</div>
                <div class="badges">
                    <span class="badge">MySQL</span>
                    <span class="badge">SQL</span>
                    <span class="badge">PL/SQL</span>
                    <span class="badge">NoSQL</span>
                </div>
            </div>

            <div class="stack-group">
                <div class="stack-label">Tools & Environment</div>
                <div class="badges">
                    <span class="badge">Git</span>
                    <span class="badge">GitHub</span>
                    <span class="badge">Linux</span>
                    <span class="badge">Arch Linux</span>
                    <span class="badge">VS Code</span>
                    <span class="badge">Docker</span>
                </div>
            </div>
        </div>

        <!-- Areas of Focus -->
        <div class="section">
            <h2 class="section-title">Areas of Focus</h2>
            <div class="grid">
                <div class="card">
                    <div class="card-title">Backend</div>
                    <div class="card-content">
                        APIs robustas, arquitetura escalável e lógica de aplicação eficiente. Construindo serviços que funcionam sob pressão.
                    </div>
                </div>
                <div class="card">
                    <div class="card-title">Linux & Systems</div>
                    <div class="card-content">
                        Configuração, automação e compreensão profunda de como os sistemas operacionais funcionam. Arch Linux é meu playground.
                    </div>
                </div>
                <div class="card">
                    <div class="card-title">Databases</div>
                    <div class="card-content">
                        Design relacional, otimização de queries e modelagem de dados. Dados bem estruturados = aplicações melhores.
                    </div>
                </div>
                <div class="card">
                    <div class="card-title">Cybersecurity</div>
                    <div class="card-content">
                        Segurança web, hardening de sistemas e pesquisa de vulnerabilidades. Entender ameaças é essencial para defendê-las.
                    </div>
                </div>
                <div class="card">
                    <div class="card-title">Open Source</div>
                    <div class="card-content">
                        Contribuindo ao ecossistema de software livre. Código compartilhado, inspecionado, melhorado por muitos.
                    </div>
                </div>
                <div class="card">
                    <div class="card-title">Web Development</div>
                    <div class="card-content">
                        Interfaces responsivas e performáticas. Combinando design com funcionalidade robusta.
                    </div>
                </div>
            </div>
        </div>

        <!-- Learning Path -->
        <div class="section">
            <h2 class="section-title">Learning Philosophy</h2>
            <div class="process-flow">
                <div class="process-step">
                    <div class="step-circle">01</div>
                    <div class="step-title">Learn</div>
                </div>
                <div class="process-arrow">→</div>
                <div class="process-step">
                    <div class="step-circle">02</div>
                    <div class="step-title">Build</div>
                </div>
                <div class="process-arrow">→</div>
                <div class="process-step">
                    <div class="step-circle">03</div>
                    <div class="step-title">Experiment</div>
                </div>
                <div class="process-arrow">→</div>
                <div class="process-step">
                    <div class="step-circle">04</div>
                    <div class="step-title">Improve</div>
                </div>
            </div>
            <p style="text-align: center; margin-top: 40px; font-size: 1.05rem;">
                Minha abordagem não é acumular tecnologias por portfolio. É entender <strong>quando, por quê e como</strong> cada ferramenta deve ser aplicada.
            </p>
        </div>

        <!-- Current Goals -->
        <div class="section">
            <h2 class="section-title">Current Goals</h2>
            <div class="badges" style="justify-content: center;">
                <span class="badge">Dominar Backend Dev</span>
                <span class="badge">Kernel Linux</span>
                <span class="badge">Cybersecurity Research</span>
                <span class="badge">Open Source Contrib</span>
                <span class="badge">Build Real Products</span>
                <span class="badge">System Architecture</span>
            </div>
        </div>

        <!-- Footer -->
        <div class="footer">
            <div class="social-links">
                <a href="https://github.com/LM-btw" class="social-link">
                    GitHub
                </a>
                <a href="https://www.linkedin.com/in/lucas-matheus-torres-cardoso-6996b8273/" class="social-link">
                    LinkedIn
                </a>
            </div>
            <p style="color: var(--text-secondary); margin-bottom: 20px;">
                Software · Linux · Security · Open Source
            </p>
            <div class="quote">
                "Stay curious. Build things. Understand how they work."
            </div>
        </div>
    </div>

    <script>
        // Typing effect
        const texts = [
            "Software Developer",
            "Linux Enthusiast",
            "Cybersecurity Explorer",
            "Backend Specialist",
            "System Architect"
        ];

        let textIndex = 0;
        let charIndex = 0;
        let isDeleting = false;
        const typingSpeed = 100;
        const deletingSpeed = 50;
        const delayBetweenTexts = 2000;

        function type() {
            const currentText = texts[textIndex];
            const typingElement = document.getElementById('typingText');

            if (isDeleting) {
                typingElement.textContent = currentText.substring(0, charIndex - 1);
                charIndex--;
            } else {
                typingElement.textContent = currentText.substring(0, charIndex + 1);
                charIndex++;
            }

            if (!isDeleting && charIndex === currentText.length) {
                isDeleting = true;
                setTimeout(type, delayBetweenTexts);
            } else if (isDeleting && charIndex === 0) {
                isDeleting = false;
                textIndex = (textIndex + 1) % texts.length;
                setTimeout(type, 500);
            } else {
                setTimeout(type, isDeleting ? deletingSpeed : typingSpeed);
            }
        }

        type();

        // Add stagger animation to badges
        const badges = document.querySelectorAll('.badge');
        badges.forEach((badge, index) => {
            badge.style.animationDelay = `${index * 0.1}s`;
        });

        // Add interaction feedback
        document.querySelectorAll('.card').forEach(card => {
            card.addEventListener('mouseenter', function() {
                this.style.borderColor = 'var(--secondary)';
            });
            card.addEventListener('mouseleave', function() {
                this.style.borderColor = 'var(--primary)';
            });
        });
    </script>
</body>
</html>
