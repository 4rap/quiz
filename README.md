<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Quiz Sejarah - Kerajaan Hindu Buddha & Islam</title>
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: #1a2a1a;
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            background-image: radial-gradient(circle at 10% 20%, #2d5a2d, #0f1a0f);
        }
        .container {
            background: #2d4a2d;
            padding: 20px;
            border-radius: 30px;
            box-shadow: 0 20px 40px rgba(0,0,0,0.7);
            width: 95%;
            max-width: 800px;
            border: 4px solid #5a7a4a;
        }
        .game-panel {
            background: #3e5e3e;
            border-radius: 20px;
            padding: 20px;
            color: #f0e6d0;
            box-shadow: inset 0 0 20px #1e3a1e;
            min-height: 550px;
            position: relative;
        }
        h1, h2 {
            text-align: center;
            color: #f5d742;
            text-shadow: 3px 3px 0 #3a5a1a;
            letter-spacing: 2px;
            margin-bottom: 15px;
        }
        h2 {
            font-size: 1.5rem;
            color: #e6c87a;
        }
        .menu-screen, .char-select, .difficulty-select, .game-screen, .result-screen {
            display: none;
            animation: fadeIn 0.4s ease;
        }
        .active {
            display: block;
        }
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }
        .btn {
            background: #d4a843;
            border: none;
            color: #1e2a1e;
            font-weight: bold;
            padding: 12px 28px;
            border-radius: 40px;
            font-size: 1.2rem;
            cursor: pointer;
            transition: 0.2s;
            box-shadow: 0 6px 0 #7a5a1a;
            margin: 8px;
            border: 2px solid #f5e07a;
        }
        .btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 9px 0 #7a5a1a;
            background: #ecc45a;
        }
        .btn:active {
            transform: translateY(5px);
            box-shadow: 0 2px 0 #7a5a1a;
        }
        .btn-small {
            padding: 8px 16px;
            font-size: 1rem;
        }
        .avatar-grid {
            display: grid;
            grid-template-columns: repeat(5, 1fr);
            gap: 10px;
            margin: 20px 0;
        }
        .avatar-item {
            background: #3c553c;
            border-radius: 20px;
            padding: 10px 5px;
            text-align: center;
            cursor: pointer;
            border: 3px solid transparent;
            transition: 0.2s;
            box-shadow: 0 4px 0 #1f2f1f;
        }
        .avatar-item.selected {
            border-color: #f5d742;
            background: #5a7a4a;
            box-shadow: 0 0 15px #f5d742;
        }
        .avatar-item span {
            font-size: 3.5rem;
            display: block;
        }
        .avatar-item .gender {
            font-size: 0.8rem;
            color: #bbb;
        }
        .input-name {
            background: #1f301f;
            border: 2px solid #7a9a5a;
            color: #f0e6d0;
            padding: 10px 15px;
            border-radius: 30px;
            font-size: 1.1rem;
            width: 70%;
            margin: 10px auto;
            display: block;
            text-align: center;
        }
        .input-name:focus {
            outline: none;
            border-color: #f5d742;
        }
        .difficulty-buttons {
            display: flex;
            justify-content: center;
            flex-wrap: wrap;
            gap: 15px;
            margin: 20px 0;
        }
        .diff-btn {
            background: #3a5a3a;
            border: 3px solid #7a9a5a;
            padding: 15px 30px;
            border-radius: 60px;
            font-size: 1.3rem;
            font-weight: bold;
            color: #f0e6d0;
            cursor: pointer;
            transition: 0.2s;
            min-width: 120px;
        }
        .diff-btn:hover {
            background: #5a7a4a;
            transform: scale(1.05);
        }
        .diff-btn.easy { border-color: #6ab04c; color: #b8e6a0; }
        .diff-btn.medium { border-color: #f5a742; color: #f5d742; }
        .diff-btn.hard { border-color: #e74c3c; color: #f5a0a0; }
        .game-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            background: #1f301f;
            padding: 10px 20px;
            border-radius: 50px;
            margin-bottom: 15px;
            flex-wrap: wrap;
        }
        .game-header .char-info {
            display: flex;
            align-items: center;
            gap: 10px;
        }
        .game-header .char-info span {
            font-size: 2rem;
        }
        .progress-bar {
            background: #1f301f;
            height: 12px;
            border-radius: 20px;
            margin: 10px 0;
            overflow: hidden;
            border: 2px solid #5a7a4a;
        }
        .progress-fill {
            height: 100%;
            background: #f5d742;
            width: 0%;
            transition: 0.3s;
            border-radius: 20px;
        }
        .question-text {
            font-size: 1.4rem;
            background: #1f301f;
            padding: 15px;
            border-radius: 20px;
            margin: 15px 0;
            border-left: 8px solid #f5d742;
        }
        .options {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 10px;
            margin: 15px 0;
        }
        .option-btn {
            background: #2a442a;
            border: 2px solid #5a7a4a;
            color: #f0e6d0;
            padding: 12px;
            border-radius: 30px;
            font-size: 1rem;
            cursor: pointer;
            transition: 0.2s;
            text-align: left;
            padding-left: 20px;
        }
        .option-btn:hover {
            background: #4a6a3a;
            border-color: #f5d742;
        }
        .option-btn.correct {
            background: #2e7d32;
            border-color: #81c784;
        }
        .option-btn.wrong {
            background: #b71c1c;
            border-color: #ef9a9a;
        }
        .option-btn:disabled {
            opacity: 0.7;
            cursor: not-allowed;
        }
        .map-area {
            background: #1f3a1f;
            border-radius: 30px;
            padding: 10px;
            margin: 15px 0;
            border: 4px solid #5a7a4a;
            background-image: linear-gradient(45deg, #2d5a2d 25%, #1f3a1f 25%, #1f3a1f 50%, #2d5a2d 50%, #2d5a2d 75%, #1f3a1f 75%, #1f3a1f 100%);
            background-size: 40px 40px;
            position: relative;
            min-height: 80px;
            display: flex;
            align-items: center;
            justify-content: center;
        }
        .map-text {
            background: rgba(0,0,0,0.6);
            padding: 10px 20px;
            border-radius: 40px;
            font-size: 1.2rem;
            backdrop-filter: blur(4px);
            border: 2px solid #7a9a5a;
        }
        .map-text .step {
            color: #f5d742;
            font-weight: bold;
        }
        .footer-buttons {
            display: flex;
            justify-content: center;
            gap: 10px;
            flex-wrap: wrap;
            margin-top: 15px;
        }
        .result-box {
            text-align: center;
            padding: 20px;
        }
        .result-box .big-score {
            font-size: 4rem;
            font-weight: bold;
            color: #f5d742;
        }
        .avatar-preview {
            font-size: 4rem;
            display: inline-block;
            margin: 10px;
        }
        @media (max-width: 600px) {
            .options { grid-template-columns: 1fr; }
            .avatar-grid { grid-template-columns: repeat(3, 1fr); }
        }
        .hidden { display: none; }
    </style>
</head>
<body>
<div class="container">
    <div class="game-panel">
        <!-- MENU UTAMA -->
        <div id="menuScreen" class="menu-screen active">
            <h1>🏰 PETA SEJARAH</h1>
            <h2>Kerajaan Hindu-Buddha & Islam</h2>
            <div style="text-align:center; margin: 30px 0;">
                <div style="font-size:5rem;">🗺️</div>
                <p style="font-style:italic; color:#b8d0a0;">Jelajahi hutan & kuil sejarah</p>
            </div>
            <div style="text-align:center;">
                <button class="btn" id="playBtn">▶ MAIN</button>
            </div>
        </div>

        <!-- PILIH KARAKTER -->
        <div id="charScreen" class="char-select">
            <h2>👤 Pilih Karakter</h2>
            <div class="avatar-grid" id="avatarGrid"></div>
            <input type="text" class="input-name" id="charNameInput" placeholder="Beri nama karaktermu..." maxlength="15">
            <div style="text-align:center;">
                <button class="btn btn-small" id="confirmCharBtn">✔ Pilih & Lanjut</button>
            </div>
        </div>

        <!-- PILIH LEVEL -->
        <div id="diffScreen" class="difficulty-select">
            <h2>⚔ Pilih Level</h2>
            <div style="text-align:center; margin:10px 0;">
                <span id="diffCharPreview" style="font-size:3rem;"></span>
                <span id="diffCharName" style="font-size:1.5rem; display:block;"></span>
            </div>
            <div class="difficulty-buttons">
                <button class="diff-btn easy" data-diff="easy">🌱 Easy</button>
                <button class="diff-btn medium" data-diff="medium">🌿 Medium</button>
                <button class="diff-btn hard" data-diff="hard">🔥 Hard</button>
            </div>
        </div>

        <!-- GAME SCREEN -->
        <div id="gameScreen" class="game-screen">
            <div class="game-header">
                <div class="char-info">
                    <span id="gameAvatar"></span>
                    <span id="gameCharName"></span>
                </div>
                <div>🗺️ Level: <span id="gameLevelDisplay"></span></div>
            </div>
            <div class="progress-bar">
                <div class="progress-fill" id="progressFill"></div>
            </div>
            <div class="map-area">
                <div class="map-text" id="mapText">🌳 <span class="step">Hutan</span> — Langkah 1</div>
            </div>
            <div class="question-text" id="questionText">Memuat pertanyaan...</div>
            <div class="options" id="optionsContainer"></div>
            <div class="footer-buttons">
                <button class="btn btn-small" id="nextLevelBtn" style="display:none;">➡ Level Selanjutnya</button>
                <button class="btn btn-small" id="restartGameBtn">↺ Restart</button>
            </div>
        </div>

        <!-- HASIL -->
        <div id="resultScreen" class="result-screen">
            <div class="result-box">
                <h2>🏁 Perjalanan Selesai!</h2>
                <div class="avatar-preview" id="resultAvatar"></div>
                <div id="resultName" style="font-size:1.8rem;"></div>
                <div class="big-score" id="resultScore">0</div>
                <div style="font-size:1.2rem;">Benar dari <span id="resultTotal"></span> pertanyaan</div>
                <div style="margin-top:20px;">
                    <button class="btn" id="backToMenuBtn">🏠 Kembali ke Menu</button>
                </div>
            </div>
        </div>
    </div>
</div>

<script>
    // ===================== DATA =====================
    const avatars = [
        { emoji: '🧝', gender: 'Laki-laki', name: 'Elang' },
        { emoji: '🧙', gender: 'Laki-laki', name: 'Bayu' },
        { emoji: '🦸', gender: 'Laki-laki', name: 'Satria' },
        { emoji: '🤴', gender: 'Laki-laki', name: 'Raja' },
        { emoji: '🥷', gender: 'Laki-laki', name: 'Krisna' },
        { emoji: '🧝‍♀️', gender: 'Perempuan', name: 'Dewi' },
        { emoji: '🧙‍♀️', gender: 'Perempuan', name: 'Ratri' },
        { emoji: '🦸‍♀️', gender: 'Perempuan', name: 'Gadis' },
        { emoji: '👸', gender: 'Perempuan', name: 'Ratu' },
        { emoji: '🥷‍♀️', gender: 'Perempuan', name: 'Sari' }
    ];

    // 5 level, masing-masing 3 pertanyaan (total 15 pertanyaan)
    const questions = [
        // Level 1 (Hindu-Buddha)
        { level: 1, q: "Kerajaan Hindu tertua di Indonesia adalah?", options: ["Kutai", "Tarumanegara", "Mataram Kuno", "Sriwijaya"], correct: 0, map: "🌳 Hutan Tropis - Candi Batu" },
        { level: 1, q: "Candi Borobudur dibangun pada masa kerajaan?", options: ["Mataram Kuno", "Kediri", "Majapahit", "Singasari"], correct: 0, map: "🏛️ Candi Borobudur" },
        { level: 1, q: "Kerajaan yang bercorak Buddha di Sumatera adalah?", options: ["Sriwijaya", "Majapahit", "Kutai", "Tarumanegara"], correct: 0, map: "🌊 Sungai Musi - Sriwijaya" },
        // Level 2 (Hindu-Buddha lanjut)
        { level: 2, q: "Raja terbesar Kerajaan Majapahit adalah?", options: ["Hayam Wuruk", "Gajah Mada", "Kertanegara", "Ken Arok"], correct: 0, map: "🏯 Trowulan - Majapahit" },
        { level: 2, q: "Kerajaan Mataram Kuno terpecah menjadi dua, yaitu?", options: ["Medang dan Kahuripan", "Kediri dan Jenggala", "Singasari dan Majapahit", "Pajajaran dan Galuh"], correct: 1, map: "🗺️ Peta Jawa Tengah" },
        { level: 2, q: "Candi Prambanan adalah candi bercorak?", options: ["Hindu (Siwa)", "Buddha", "Konghucu", "Animisme"], correct: 0, map: "🏛️ Candi Prambanan" },
        // Level 3 (Islam awal)
        { level: 3, q: "Kerajaan Islam pertama di Jawa adalah?", options: ["Demak", "Banten", "Cirebon", "Mataram Islam"], correct: 0, map: "🕌 Masjid Agung Demak" },
        { level: 3, q: "Wali Songo yang menyebarkan Islam di Jawa, salah satunya adalah?", options: ["Sunan Kalijaga", "Sultan Agung", "Pangeran Diponegoro", "Hamengkubuwono"], correct: 0, map: "🌅 Pantai Utara Jawa" },
        { level: 3, q: "Kerajaan Islam di Sumatera yang terkenal adalah?", options: ["Samudera Pasai", "Aceh Darussalam", "Malaka", "Demak"], correct: 0, map: "🌊 Selat Malaka" },
        // Level 4 (Islam lanjut)
        { level: 4, q: "Sultan Agung adalah raja dari kerajaan?", options: ["Mataram Islam", "Demak", "Banten", "Cirebon"], correct: 0, map: "🏞️ Gunung Merapi" },
        { level: 4, q: "Kerajaan Islam di Sulawesi yang terkenal adalah?", options: ["Gowa-Tallo", "Ternate", "Tidore", "Bone"], correct: 0, map: "🏝️ Sulawesi Selatan" },
        { level: 4, q: "Penyebar agama Islam di Jawa yang terkenal dengan sebutan Sunan?", options: ["Sunan Bonang", "Sunan Muria", "Sunan Gunungjati", "Sunan Ampel"], correct: 0, map: "🌾 Sawah - Jawa Timur" },
        // Level 5 (Campuran dan akhir)
        { level: 5, q: "Kerajaan bercorak Hindu-Buddha terbesar di Indonesia adalah?", options: ["Majapahit", "Sriwijaya", "Mataram Kuno", "Singasari"], correct: 0, map: "🌋 Gunung Bromo" },
        { level: 5, q: "Peninggalan sejarah kerajaan Islam berupa?", options: ["Masjid & Makam", "Candi & Prasasti", "Arca & Patung", "Kitab Weda"], correct: 0, map: "🕋 Masjid Agung" },
        { level: 5, q: "Raja Samudera Pasai yang terkenal adalah?", options: ["Malik al-Saleh", "Sultan Iskandar Muda", "Sultan Agung", "Prabu Hayam Wuruk"], correct: 0, map: "⛵ Pelabuhan Pasai" }
    ];

    // ===================== STATE =====================
    let state = {
        currentScreen: 'menu',
        selectedAvatarIndex: 0,
        charName: '',
        difficulty: 'easy', // easy, medium, hard
        currentLevel: 1,    // 1-5
        currentQuestionInLevel: 0, // 0-2
        score: 0,
        totalAnswered: 0,
        answered: false,
        usedQuestions: [], // indices yang sudah dipakai di level ini
        levelQuestions: [], // 3 pertanyaan untuk level saat ini
    };

    // ===================== DOM REFS =====================
    const menuScreen = document.getElementById('menuScreen');
    const charScreen = document.getElementById('charScreen');
    const diffScreen = document.getElementById('diffScreen');
    const gameScreen = document.getElementById('gameScreen');
    const resultScreen = document.getElementById('resultScreen');
    const avatarGrid = document.getElementById('avatarGrid');
    const charNameInput = document.getElementById('charNameInput');
    const confirmCharBtn = document.getElementById('confirmCharBtn');
    const diffCharPreview = document.getElementById('diffCharPreview');
    const diffCharName = document.getElementById('diffCharName');
    const gameAvatar = document.getElementById('gameAvatar');
    const gameCharName = document.getElementById('gameCharName');
    const gameLevelDisplay = document.getElementById('gameLevelDisplay');
    const progressFill = document.getElementById('progressFill');
    const mapText = document.getElementById('mapText');
    const questionText = document.getElementById('questionText');
    const optionsContainer = document.getElementById('optionsContainer');
    const nextLevelBtn = document.getElementById('nextLevelBtn');
    const restartGameBtn = document.getElementById('restartGameBtn');
    const backToMenuBtn = document.getElementById('backToMenuBtn');
    const resultAvatar = document.getElementById('resultAvatar');
    const resultName = document.getElementById('resultName');
    const resultScore = document.getElementById('resultScore');
    const resultTotal = document.getElementById('resultTotal');
    const playBtn = document.getElementById('playBtn');

    // ===================== FUNGSI =====================
    function showScreen(id) {
        [menuScreen, charScreen, diffScreen, gameScreen, resultScreen].forEach(el => el.classList.remove('active'));
        document.getElementById(id).classList.add('active');
    }

    function renderAvatars() {
        avatarGrid.innerHTML = '';
        avatars.forEach((av, idx) => {
            const div = document.createElement('div');
            div.className = 'avatar-item' + (idx === state.selectedAvatarIndex ? ' selected' : '');
            div.innerHTML = `<span>${av.emoji}</span><div class="gender">${av.gender}</div>`;
            div.dataset.index = idx;
            div.addEventListener('click', () => {
                document.querySelectorAll('.avatar-item').forEach(el => el.classList.remove('selected'));
                div.classList.add('selected');
                state.selectedAvatarIndex = idx;
                charNameInput.value = avatars[idx].name;
            });
            avatarGrid.appendChild(div);
        });
        // Set default name
        charNameInput.value = avatars[state.selectedAvatarIndex].name;
    }

    function startGame() {
        state.currentLevel = 1;
        state.score = 0;
        state.totalAnswered = 0;
        state.usedQuestions = [];
        showScreen('gameScreen');
        loadLevel(1);
    }

    function loadLevel(level) {
        state.currentLevel = level;
        state.currentQuestionInLevel = 0;
        state.answered = false;
        // Ambil 3 pertanyaan untuk level ini
        const pool = questions.filter(q => q.level === level);
        // Jika kurang dari 3, pakai semua (tapi kita punya 3 per level)
        state.levelQuestions = pool.slice(0, 3);
        // Update UI
        gameLevelDisplay.textContent = level;
        const avatar = avatars[state.selectedAvatarIndex];
        gameAvatar.textContent = avatar.emoji;
        gameCharName.textContent = state.charName || avatar.name;
        // Progress
        const totalLevels = 5;
        const progress = ((level - 1) / totalLevels) * 100;
        progressFill.style.width = Math.min(progress, 100) + '%';
        // Map
        if (state.levelQuestions.length > 0) {
            mapText.innerHTML = `🗺️ ${state.levelQuestions[0].map} — Level ${level}`;
        }
        nextLevelBtn.style.display = 'none';
        showQuestion();
    }

    function showQuestion() {
        if (state.currentQuestionInLevel >= state.levelQuestions.length) {
            // Level selesai
            if (state.currentLevel < 5) {
                nextLevelBtn.style.display = 'inline-block';
                mapText.innerHTML = `✅ Level ${state.currentLevel} selesai! Lanjut ke level ${state.currentLevel+1}`;
                optionsContainer.innerHTML = '';
                questionText.textContent = 'Selamat! Klik "Level Selanjutnya" untuk melanjutkan.';
                return;
            } else {
                // Game selesai
                endGame();
                return;
            }
        }

        const q = state.levelQuestions[state.currentQuestionInLevel];
        questionText.textContent = q.q;
        optionsContainer.innerHTML = '';
        q.options.forEach((opt, idx) => {
            const btn = document.createElement('button');
            btn.className = 'option-btn';
            btn.textContent = String.fromCharCode(65 + idx) + '. ' + opt;
            btn.dataset.index = idx;
            btn.addEventListener('click', () => handleAnswer(idx, q.correct, btn));
            optionsContainer.appendChild(btn);
        });
        // Update map
        mapText.innerHTML = `🗺️ ${q.map} — Level ${state.currentLevel}`;
        state.answered = false;
    }

    function handleAnswer(selected, correct, btnElement) {
        if (state.answered) return;
        state.answered = true;
        state.totalAnswered++;
        const allBtns = optionsContainer.querySelectorAll('.option-btn');
        allBtns.forEach((btn, idx) => {
            btn.disabled = true;
            if (idx === correct) btn.classList.add('correct');
            if (idx === selected && idx !== correct) btn.classList.add('wrong');
        });
        if (selected === correct) {
            state.score++;
        }
        // Progress after answer
        setTimeout(() => {
            state.currentQuestionInLevel++;
            showQuestion();
        }, 1200);
    }

    function endGame() {
        showScreen('resultScreen');
        const avatar = avatars[state.selectedAvatarIndex];
        resultAvatar.textContent = avatar.emoji;
        resultName.textContent = state.charName || avatar.name;
        resultScore.textContent = state.score;
        resultTotal.textContent = state.totalAnswered;
        progressFill.style.width = '100%';
    }

    // ===================== EVENT LISTENERS =====================
    playBtn.addEventListener('click', () => {
        state.charName = '';
        renderAvatars();
        showScreen('charScreen');
    });

    confirmCharBtn.addEventListener('click', () => {
        const name = charNameInput.value.trim();
        if (name === '') {
            alert('Masukkan nama karaktermu!');
            return;
        }
        state.charName = name;
        const avatar = avatars[state.selectedAvatarIndex];
        diffCharPreview.textContent = avatar.emoji;
        diffCharName.textContent = `${name} (${avatar.gender})`;
        showScreen('diffScreen');
    });

    // Difficulty buttons
    document.querySelectorAll('.diff-btn').forEach(btn => {
        btn.addEventListener('click', () => {
            state.difficulty = btn.dataset.diff;
            // Sesuaikan jumlah pertanyaan? Di sini kita tetap sama, hanya "feel" saja.
            // Tapi kita bisa memberi tahu pemain.
            startGame();
        });
    });

    nextLevelBtn.addEventListener('click', () => {
        if (state.currentLevel < 5) {
            loadLevel(state.currentLevel + 1);
        } else {
            endGame();
        }
    });

    restartGameBtn.addEventListener('click', () => {
        if (confirm('Restart permainan? Progress akan hilang.')) {
            startGame();
        }
    });

    backToMenuBtn.addEventListener('click', () => {
        showScreen('menuScreen');
        progressFill.style.width = '0%';
    });

    // Inisialisasi
    renderAvatars();
    showScreen('menuScreen');

    // Tambahan: jika pengguna langsung klik diff tanpa pilih karakter? kita sudah atur.
    // Pastikan state charName terisi.
</script>
</body>
</html>
