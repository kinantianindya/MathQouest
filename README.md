<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Game Matematika Dasar</title>
    <style>
        :root {
            --bg: #0f0c29;
            --bg2: #1a1a3e;
            --card: #1e1e4a;
            --primary: #6c5ce7;
            --primary-light: #a29bfe;
            --success: #00b894;
            --danger: #e17055;
            --warning: #fdcb6e;
            --text: #dfe6e9;
            --text-dark: #2d3436;
            --gold: #ffd700;
            --border: #3a3a6e;
            --shadow: 0 8px 32px rgba(0, 0, 0, 0.4);
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', 'Poppins', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #0f0c29, #1a1a3e 40%, #24243e 100%);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
            user-select: none;
            -webkit-tap-highlight-color: transparent;
        }

        /* Background animasi partikel */
        .particles {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 0;
            overflow: hidden;
        }
        .particle {
            position: absolute;
            background: rgba(108, 92, 231, 0.3);
            border-radius: 50%;
            animation: floatUp linear infinite;
        }
        @keyframes floatUp {
            0% {
                transform: translateY(100vh) scale(0);
                opacity: 0;
            }
            10% {
                opacity: 1;
            }
            90% {
                opacity: 1;
            }
            100% {
                transform: translateY(-100px) scale(1.5);
                opacity: 0;
            }
        }

        .game-container {
            position: relative;
            z-index: 1;
            background: var(--card);
            border-radius: 24px;
            padding: 30px 28px;
            max-width: 500px;
            width: 100%;
            box-shadow: var(--shadow), 0 0 60px rgba(108, 92, 231, 0.15);
            border: 1px solid var(--border);
            transition: all 0.3s ease;
        }

        /* Header */
        .game-header {
            text-align: center;
            margin-bottom: 24px;
        }
        .game-header h1 {
            font-size: 1.8em;
            font-weight: 700;
            background: linear-gradient(135deg, #a29bfe, #ffd700);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            margin-bottom: 4px;
            letter-spacing: 1px;
        }
        .game-header .subtitle {
            color: #a0a0c8;
            font-size: 0.85em;
            letter-spacing: 2px;
            text-transform: uppercase;
        }

        /* Info bar */
        .info-bar {
            display: flex;
            justify-content: space-between;
            align-items: center;
            flex-wrap: wrap;
            gap: 10px;
            margin-bottom: 20px;
            background: rgba(0, 0, 0, 0.25);
            border-radius: 16px;
            padding: 14px 18px;
        }
        .info-item {
            display: flex;
            align-items: center;
            gap: 8px;
            color: var(--text);
            font-weight: 600;
            font-size: 0.95em;
        }
        .info-item .icon {
            font-size: 1.3em;
        }
        .score-value {
            color: var(--gold);
            font-size: 1.3em;
            font-weight: 700;
            text-shadow: 0 0 20px rgba(255, 215, 0, 0.5);
        }
        .streak-badge {
            background: linear-gradient(135deg, #e17055, #fd7e4e);
            color: #fff;
            border-radius: 20px;
            padding: 4px 12px;
            font-size: 0.8em;
            font-weight: 700;
            animation: pulse 1.5s ease-in-out infinite;
        }
        @keyframes pulse {
            0%,
            100% {
                transform: scale(1);
            }
            50% {
                transform: scale(1.08);
            }
        }

        /* Question area */
        .question-area {
            text-align: center;
            padding: 30px 20px;
            background: rgba(0, 0, 0, 0.3);
            border-radius: 20px;
            margin-bottom: 22px;
            border: 2px dashed var(--border);
            position: relative;
            overflow: hidden;
        }
        .operation-badge {
            display: inline-block;
            background: var(--primary);
            color: #fff;
            border-radius: 20px;
            padding: 5px 16px;
            font-size: 0.8em;
            font-weight: 700;
            letter-spacing: 1px;
            margin-bottom: 12px;
            text-transform: uppercase;
        }
        .question-text {
            font-size: 2.8em;
            font-weight: 800;
            color: #fff;
            letter-spacing: 2px;
            word-break: break-all;
            text-shadow: 0 0 30px rgba(255, 255, 255, 0.3);
            transition: all 0.3s ease;
        }
        .question-text.shake {
            animation: shake 0.6s ease-in-out;
        }
        @keyframes shake {
            0%,
            100% {
                transform: translateX(0);
            }
            20% {
                transform: translateX(-12px);
            }
            40% {
                transform: translateX(12px);
            }
            60% {
                transform: translateX(-8px);
            }
            80% {
                transform: translateX(5px);
            }
        }

        /* Tombol operasi */
        .operation-selector {
            display: flex;
            flex-wrap: wrap;
            gap: 8px;
            justify-content: center;
            margin-bottom: 20px;
        }
        .op-btn {
            background: rgba(255, 255, 255, 0.06);
            border: 2px solid var(--border);
            color: #b0b0d0;
            padding: 10px 15px;
            border-radius: 25px;
            cursor: pointer;
            font-weight: 600;
            font-size: 0.85em;
            transition: all 0.25s ease;
            letter-spacing: 0.5px;
            white-space: nowrap;
        }
        .op-btn:hover {
            background: rgba(108, 92, 231, 0.2);
            border-color: var(--primary-light);
            color: #fff;
            transform: translateY(-2px);
        }
        .op-btn.active {
            background: var(--primary);
            border-color: var(--primary-light);
            color: #fff;
            box-shadow: 0 4px 20px rgba(108, 92, 231, 0.5);
            font-weight: 700;
        }

        /* Answer buttons */
        .answers-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 12px;
            margin-bottom: 20px;
        }
        .answer-btn {
            background: rgba(255, 255, 255, 0.05);
            border: 2px solid var(--border);
            color: var(--text);
            padding: 16px;
            border-radius: 16px;
            cursor: pointer;
            font-size: 1.2em;
            font-weight: 700;
            transition: all 0.2s ease;
            position: relative;
            overflow: hidden;
            letter-spacing: 1px;
        }
        .answer-btn:hover {
            background: rgba(108, 92, 231, 0.2);
            border-color: var(--primary-light);
            transform: translateY(-3px);
            box-shadow: 0 8px 25px rgba(0, 0, 0, 0.3);
        }
        .answer-btn:active {
            transform: scale(0.95);
        }
        .answer-btn.correct {
            background: var(--success) !important;
            border-color: #55efc4 !important;
            color: #fff !important;
            animation: popCorrect 0.5s ease;
            box-shadow: 0 0 30px rgba(0, 184, 148, 0.6) !important;
        }
        .answer-btn.wrong {
            background: var(--danger) !important;
            border-color: #ff7675 !important;
            color: #fff !important;
            animation: shake 0.5s ease;
        }
        .answer-btn.disabled {
            pointer-events: none;
            opacity: 0.7;
        }
        @keyframes popCorrect {
            0% {
                transform: scale(1);
            }
            30% {
                transform: scale(1.12);
            }
            100% {
                transform: scale(1);
            }
        }

        /* Feedback */
        .feedback {
            text-align: center;
            font-weight: 700;
            font-size: 1.1em;
            min-height: 28px;
            transition: all 0.3s ease;
            letter-spacing: 1px;
        }
        .feedback.correct-fb {
            color: #55efc4;
            text-shadow: 0 0 15px rgba(0, 184, 148, 0.5);
        }
        .feedback.wrong-fb {
            color: #ff7675;
            text-shadow: 0 0 15px rgba(225, 112, 85, 0.5);
        }

        /* Tombol next */
        .next-btn {
            display: block;
            margin: 16px auto 0;
            background: linear-gradient(135deg, #6c5ce7, #a29bfe);
            color: #fff;
            border: none;
            padding: 14px 36px;
            border-radius: 30px;
            cursor: pointer;
            font-weight: 700;
            font-size: 1em;
            letter-spacing: 1px;
            transition: all 0.3s ease;
            box-shadow: 0 6px 20px rgba(108, 92, 231, 0.4);
            display: none;
        }
        .next-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 10px 30px rgba(108, 92, 231, 0.6);
        }
        .next-btn:active {
            transform: scale(0.95);
        }

        /* Confetti */
        .confetti-container {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 99;
        }
        .confetti-piece {
            position: absolute;
            width: 12px;
            height: 12px;
            border-radius: 3px;
            animation: confettiFall linear forwards;
        }
        @keyframes confettiFall {
            0% {
                transform: translateY(-100px) rotate(0deg) scale(1);
                opacity: 1;
            }
            100% {
                transform: translateY(110vh) rotate(720deg) scale(0.3);
                opacity: 0;
            }
        }

        /* Responsive */
        @media (max-width: 480px) {
            .game-container {
                padding: 20px 16px;
                border-radius: 18px;
            }
            .question-text {
                font-size: 2.2em;
            }
            .answers-grid {
                grid-template-columns: 1fr 1fr;
                gap: 8px;
            }
            .answer-btn {
                padding: 14px;
                font-size: 1em;
                border-radius: 12px;
            }
            .game-header h1 {
                font-size: 1.4em;
            }
            .op-btn {
                padding: 8px 11px;
                font-size: 0.75em;
            }
        }
    </style>
</head>
<body>

    <!-- Partikel background -->
    <div class="particles" id="particles"></div>

    <!-- Container Game -->
    <div class="game-container">
        <!-- Header -->
        <div class="game-header">
            <h1>🧮 Math Quest</h1>
            <p class="subtitle">Game Matematika Dasar</p>
        </div>

        <!-- Info Bar -->
        <div class="info-bar">
            <div class="info-item">
                <span class="icon">⭐</span>
                <span>Skor: </span>
                <span class="score-value" id="scoreDisplay">0</span>
            </div>
            <div class="info-item">
                <span class="icon">🔥</span>
                <span>Streak: </span>
                <span class="streak-badge" id="streakDisplay">0</span>
            </div>
            <div class="info-item">
                <span class="icon">✅</span>
                <span>Benar: </span>
                <span id="correctCount">0</span>
            </div>
        </div>

        <!-- Tombol Operasi -->
        <div class="operation-selector" id="operationSelector">
            <button class="op-btn active" data-op="all">🎲 Semua</button>
            <button class="op-btn" data-op="+">➕ Tambah</button>
            <button class="op-btn" data-op="-">➖ Kurang</button>
            <button class="op-btn" data-op="×">✖ Kali</button>
            <button class="op-btn" data-op="÷">➗ Bagi</button>
            <button class="op-btn" data-op="√">√ Akar</button>
        </div>

        <!-- Area Soal -->
        <div class="question-area">
            <span class="operation-badge" id="operationBadge">🎲 SEMUA</span>
            <div class="question-text" id="questionText">12 × 8 = ?</div>
        </div>

        <!-- Pilihan Jawaban -->
        <div class="answers-grid" id="answersGrid">
            <button class="answer-btn">96</button>
            <button class="answer-btn">94</button>
            <button class="answer-btn">100</button>
            <button class="answer-btn">88</button>
        </div>

        <!-- Feedback -->
        <div class="feedback" id="feedback"></div>

        <!-- Tombol Next -->
        <button class="next-btn" id="nextBtn">▶ Lanjut Soal Berikutnya</button>
    </div>

    <!-- Confetti Container -->
    <div class="confetti-container" id="confettiContainer"></div>

    <script>
        (function() {
            // ============ STATE ============
            let score = 0;
            let streak = 0;
            let correctCount = 0;
            let currentOperation = 'all'; // 'all', '+', '-', '×', '÷', '√'
            let currentAnswer = null;
            let currentQuestion = '';
            let isAnswered = false;
            let currentOperationType = ''; // tipe operasi untuk soal saat ini

            // ============ DOM ELEMENTS ============
            const scoreDisplay = document.getElementById('scoreDisplay');
            const streakDisplay = document.getElementById('streakDisplay');
            const correctCountDisplay = document.getElementById('correctCount');
            const questionText = document.getElementById('questionText');
            const operationBadge = document.getElementById('operationBadge');
            const answersGrid = document.getElementById('answersGrid');
            const feedback = document.getElementById('feedback');
            const nextBtn = document.getElementById('nextBtn');
            const operationSelector = document.getElementById('operationSelector');
            const confettiContainer = document.getElementById('confettiContainer');
            const particlesContainer = document.getElementById('particles');

            // ============ PARTICLE BACKGROUND ============
            function createParticles() {
                particlesContainer.innerHTML = '';
                for (let i = 0; i < 35; i++) {
                    const particle = document.createElement('div');
                    particle.classList.add('particle');
                    const size = Math.random() * 8 + 3;
                    particle.style.width = size + 'px';
                    particle.style.height = size + 'px';
                    particle.style.left = Math.random() * 100 + '%';
                    particle.style.animationDuration = (Math.random() * 10 + 8) + 's';
                    particle.style.animationDelay = Math.random() * 10 + 's';
                    particle.style.opacity = Math.random() * 0.5 + 0.1;
                    const colors = [
                        'rgba(108, 92, 231, 0.4)',
                        'rgba(162, 155, 254, 0.3)',
                        'rgba(255, 215, 0, 0.25)',
                        'rgba(0, 184, 148, 0.3)',
                        'rgba(225, 112, 85, 0.25)',
                    ];
                    particle.style.background = colors[Math.floor(Math.random() * colors.length)];
                    particlesContainer.appendChild(particle);
                }
            }
            createParticles();

            // ============ CONFETTI ============
            function spawnConfetti() {
                const colors = ['#ffd700', '#ff6b6b', '#48dbfb', '#ff9ff3', '#54a0ff',
                    '#5f27cd', '#01a3a4', '#feca57', '#ff6348', '#7bed9f',
                    '#70a1ff', '#ff4757', '#2ed573', '#ffa502'
                ];
                const fragment = document.createDocumentFragment();
                for (let i = 0; i < 60; i++) {
                    const piece = document.createElement('div');
                    piece.classList.add('confetti-piece');
                    piece.style.left = Math.random() * 100 + '%';
                    piece.style.top = -(Math.random() * 40 + 10) + 'px';
                    piece.style.backgroundColor = colors[Math.floor(Math.random() * colors.length)];
                    piece.style.width = (Math.random() * 10 + 8) + 'px';
                    piece.style.height = (Math.random() * 10 + 8) + 'px';
                    piece.style.animationDuration = (Math.random() * 2 + 2) + 's';
                    piece.style.animationDelay = Math.random() * 0.5 + 's';
                    piece.style.borderRadius = Math.random() > 0.5 ? '50%' : '3px';
                    fragment.appendChild(piece);
                }
                confettiContainer.appendChild(fragment);
                setTimeout(() => {
                    confettiContainer.innerHTML = '';
                }, 3000);
            }

            // ============ UTILS ============
            function getRandomInt(min, max) {
                return Math.floor(Math.random() * (max - min + 1)) + min;
            }

            function shuffleArray(arr) {
                const shuffled = [...arr];
                for (let i = shuffled.length - 1; i > 0; i--) {
                    const j = Math.floor(Math.random() * (i + 1));
                    [shuffled[i], shuffled[j]] = [shuffled[j], shuffled[i]];
                }
                return shuffled;
            }

            // ============ GENERATE SOAL ============
            function generateQuestion() {
                let operationsPool = [];
                if (currentOperation === 'all') {
                    operationsPool = ['+', '-', '×', '÷', '√'];
                } else {
                    operationsPool = [currentOperation];
                }
                const op = operationsPool[Math.floor(Math.random() * operationsPool.length)];
                currentOperationType = op;

                let a, b, answer, questionStr;

                switch (op) {
                    case '+':
                        a = getRandomInt(5, 150);
                        b = getRandomInt(5, 150);
                        answer = a + b;
                        questionStr = `${a} + ${b} = ?`;
                        break;
                    case '-':
                        a = getRandomInt(15, 200);
                        b = getRandomInt(5, a); // hasil selalu positif
                        answer = a - b;
                        questionStr = `${a} - ${b} = ?`;
                        break;
                    case '×':
                        a = getRandomInt(2, 25);
                        b = getRandomInt(2, 15);
                        answer = a * b;
                        questionStr = `${a} × ${b} = ?`;
                        break;
                    case '÷':
                        // Hasil bagi harus bulat
                        b = getRandomInt(2, 15);
                        const quotient = getRandomInt(1, 20);
                        a = b * quotient;
                        answer = quotient;
                        questionStr = `${a} ÷ ${b} = ?`;
                        break;
                    case '√':
                        // Akar kuadrat dari bilangan kuadrat sempurna
                        const root = getRandomInt(2, 20);
                        a = root * root;
                        answer = root;
                        questionStr = `√${a} = ?`;
                        break;
                    default:
                        a = getRandomInt(5, 100);
                        b = getRandomInt(5, 100);
                        answer = a + b;
                        questionStr = `${a} + ${b} = ?`;
                }

                currentAnswer = answer;
                currentQuestion = questionStr;
                return { questionStr, answer, op };
            }

            function generateWrongAnswers(correctAnswer, op) {
                const wrongSet = new Set();
                wrongSet.add(correctAnswer);

                while (wrongSet.size < 4) {
                    let wrong;
                    const variation = Math.max(1, Math.floor(Math.abs(correctAnswer) * 0.35));
                    const offsetOptions = [
                        getRandomInt(1, variation),
                        -getRandomInt(1, variation),
                        getRandomInt(variation + 1, variation * 2),
                        -getRandomInt(variation + 1, variation * 2),
                    ];

                    // Untuk akar, variasinya lebih kecil
                    if (op === '√') {
                        const smallVar = Math.max(1, Math.floor(Math.abs(correctAnswer) * 0.25));
                        wrong = correctAnswer + (Math.random() < 0.5 ?
                            getRandomInt(1, smallVar) :
                            -getRandomInt(1, smallVar));
                    } else {
                        const offset = offsetOptions[Math.floor(Math.random() * offsetOptions.length)];
                        wrong = correctAnswer + offset;
                    }

                    // Pastikan tidak negatif (kecuali pengurangan yang sudah dihandle)
                    if (wrong < 0 && op !== '-') {
                        wrong = Math.abs(wrong) + getRandomInt(1, 5);
                    }
                    // Hindari 0 untuk pembagian dan perkalian tertentu
                    if (wrong === 0) wrong = getRandomInt(1, 10);

                    // Pastikan unik
                    if (!wrongSet.has(wrong) && wrong !== correctAnswer) {
                        wrongSet.add(wrong);
                    }
                    // Safety break
                    if (wrongSet.size > 3) break;
                }

                // Hapus jawaban benar, lalu shuffle sisanya
                wrongSet.delete(correctAnswer);
                const wrongAnswers = Array.from(wrongSet).slice(0, 3);
                // Jika kurang dari 3, tambahkan random
                while (wrongAnswers.length < 3) {
                    const r = correctAnswer + getRandomInt(5, 25) * (Math.random() < 0.5 ? 1 : -1);
                    if (r !== correctAnswer && !wrongAnswers.includes(r) && r >= 0) {
                        wrongAnswers.push(r);
                    } else {
                        wrongAnswers.push(Math.abs(r) + getRandomInt(1, 10));
                    }
                }
                return wrongAnswers.slice(0, 3);
            }

            // ============ RENDER SOAL ============
            function renderQuestion() {
                isAnswered = false;
                feedback.textContent = '';
                feedback.className = 'feedback';
                nextBtn.style.display = 'none';
                questionText.classList.remove('shake');

                const { questionStr, answer, op } = generateQuestion();

                questionText.textContent = questionStr;
                currentAnswer = answer;
                currentQuestion = questionStr;
                currentOperationType = op;

                // Update badge
                const badgeMap = {
                    '+': '➕ PENJUMLAHAN',
                    '-': '➖ PENGURANGAN',
                    '×': '✖ PERKALIAN',
                    '÷': '➗ PEMBAGIAN',
                    '√': '√ AKAR KUADRAT',
                };
                operationBadge.textContent = badgeMap[op] || '🎲 CAMPURAN';

                // Generate pilihan
                const wrongAnswers = generateWrongAnswers(answer, op);
                const allAnswers = shuffleArray([answer, ...wrongAnswers]);

                answersGrid.innerHTML = '';
                allAnswers.forEach((ans) => {
                    const btn = document.createElement('button');
                    btn.classList.add('answer-btn');
                    btn.textContent = ans;
                    btn.addEventListener('click', () => checkAnswer(ans, btn));
                    answersGrid.appendChild(btn);
                });

                // Reset semua tombol
                document.querySelectorAll('.answer-btn').forEach(b => {
                    b.classList.remove('correct', 'wrong', 'disabled');
                });
            }

            // ============ CHECK ANSWER ============
            function checkAnswer(selectedAnswer, clickedBtn) {
                if (isAnswered) return;
                isAnswered = true;

                // Disable semua tombol
                const allBtns = document.querySelectorAll('.answer-btn');
                allBtns.forEach(b => b.classList.add('disabled'));

                const isCorrect = (selectedAnswer === currentAnswer);

                if (isCorrect) {
                    // Efek benar
                    clickedBtn.classList.add('correct');
                    score += 10 + (streak * 2);
                    streak += 1;
                    correctCount += 1;
                    feedback.textContent = '🎉 Benar! Hebat sekali!';
                    feedback.className = 'feedback correct-fb';
                    questionText.style.color = '#55efc4';
                    spawnConfetti();

                    // Highlight jawaban benar jika klik bukan di jawaban benar
                    allBtns.forEach(b => {
                        if (parseInt(b.textContent) === currentAnswer) {
                            b.classList.add('correct');
                        }
                    });
                } else {
                    // Efek salah
                    clickedBtn.classList.add('wrong');
                    streak = 0;
                    feedback.textContent = `😔 Salah! Jawaban yang benar adalah ${currentAnswer}`;
                    feedback.className = 'feedback wrong-fb';
                    questionText.classList.add('shake');
                    questionText.style.color = '#ff7675';

                    // Highlight jawaban benar
                    allBtns.forEach(b => {
                        if (parseInt(b.textContent) === currentAnswer) {
                            b.classList.add('correct');
                        }
                    });

                    // Hapus shake setelah animasi
                    setTimeout(() => {
                        questionText.classList.remove('shake');
                    }, 600);
                }

                // Update display
                updateDisplay();
                nextBtn.style.display = 'block';
                nextBtn.focus();

                // Reset warna soal setelah delay
                setTimeout(() => {
                    questionText.style.color = '#fff';
                }, 800);
            }

            function updateDisplay() {
                scoreDisplay.textContent = score;
                streakDisplay.textContent = streak;
                correctCountDisplay.textContent = correctCount;

                // Animasi streak badge
                if (streak >= 5) {
                    streakDisplay.style.animation = 'pulse 0.8s ease-in-out infinite';
                } else {
                    streakDisplay.style.animation = 'pulse 1.5s ease-in-out infinite';
                }
            }

            // ============ NEXT BUTTON ============
            nextBtn.addEventListener('click', () => {
                renderQuestion();
                questionText.style.color = '#fff';
                // Scroll ke atas jika perlu
                window.scrollTo({ top: 0, behavior: 'smooth' });
            });

            // ============ OPERATION SELECTOR ============
            operationSelector.addEventListener('click', (e) => {
                if (e.target.classList.contains('op-btn')) {
                    // Update active class
                    document.querySelectorAll('.op-btn').forEach(b => b.classList.remove(
                        'active'));
                    e.target.classList.add('active');
                    // Update operation
                    currentOperation = e.target.dataset.op;
                    // Reset streak saat ganti mode
                    streak = 0;
                    updateDisplay();
                    // Render soal baru
                    renderQuestion();
                    questionText.style.color = '#fff';
                    feedback.textContent = '';
                    feedback.className = 'feedback';
                }
            });

            // ============ KEYBOARD SUPPORT ============
            document.addEventListener('keydown', (e) => {
                if (e.key === 'Enter' && isAnswered) {
                    nextBtn.click();
                }
                // Tombol 1-4 untuk memilih jawaban
                if (!isAnswered && ['1', '2', '3', '4'].includes(e.key)) {
                    const index = parseInt(e.key) - 1;
                    const btns = document.querySelectorAll('.answer-btn');
                    if (btns[index]) {
                        btns[index].click();
                    }
                }
                // Spasi untuk next
                if (e.key === ' ' && isAnswered) {
                    e.preventDefault();
                    nextBtn.click();
                }
            });

            // ============ INITIAL RENDER ============
            updateDisplay();
            renderQuestion();

            console.log('🧮 Math Quest siap!');
            console.log('  - Pilih operasi matematika');
            console.log('  - Jawab dengan klik atau tekan 1-4');
            console.log('  - Tekan Enter/Spasi untuk lanjut');
            console.log('  - Dapatkan streak untuk bonus skor!');
            console.log('✨ Selamat bermain!');
        })();
    </script>
</body>
</html>
