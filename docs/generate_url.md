<!DOCTYPE html>
<html lang="uz">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>So‘z turkumlari olamiga sayohat</title>
  <style>
    :root {
      --primary: #4f46e5;
      --primary-hover: #4338ca;
      --secondary: #06b6d4;
      --accent: #f59e0b;
      --success: #10b981;
      --danger: #ef4444;
      --bg-gradient: linear-gradient(135deg, #6366f1 0%, #a855f7 50%, #ec4899 100%);
      --card-bg: rgba(255, 255, 255, 0.95);
      --text-main: #1f2937;
      --text-muted: #4b5563;
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      user-select: none;
    }

    body {
      min-height: 100vh;
      background: var(--bg-gradient);
      display: flex;
      justify-content: center;
      align-items: center;
      padding: 12px;
      color: var(--text-main);
    }

    .game-container {
      width: 100%;
      max-width: 850px;
      background: var(--card-bg);
      border-radius: 24px;
      box-shadow: 0 20px 40px rgba(0, 0, 0, 0.25);
      padding: 24px;
      position: relative;
      overflow: hidden;
      min-height: 580px;
      display: flex;
      flex-direction: column;
      justify-content: space-between;
    }

    /* Floating background decoration */
    .bg-bubble {
      position: absolute;
      border-radius: 50%;
      background: rgba(255, 255, 255, 0.15);
      z-index: 0;
      animation: float 8s infinite ease-in-out;
      pointer-events: none;
    }
    .bubble-1 { width: 120px; height: 120px; top: -30px; left: -30px; }
    .bubble-2 { width: 90px; height: 90px; bottom: -20px; right: -20px; animation-delay: 3s; }

    @keyframes float {
      0%, 100% { transform: translateY(0) rotate(0deg); }
      50% { transform: translateY(-20px) rotate(10deg); }
    }

    header {
      z-index: 1;
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding-bottom: 16px;
      border-bottom: 2px solid #e5e7eb;
    }

    .player-info {
      font-weight: 700;
      font-size: 1.1rem;
      color: var(--primary);
    }

    .score-badge {
      background: #fef3c7;
      color: #b45309;
      padding: 6px 16px;
      border-radius: 20px;
      font-weight: 800;
      font-size: 1.1rem;
      border: 2px solid #f59e0b;
      box-shadow: 0 4px 6px rgba(0,0,0,0.05);
    }

    .screen {
      display: none;
      z-index: 1;
      flex-direction: column;
      align-items: center;
      text-align: center;
      width: 100%;
      animation: fadeIn 0.4s ease-in-out;
      margin: auto 0;
    }

    .screen.active {
      display: flex;
    }

    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(10px); }
      to { opacity: 1; transform: translateY(0); }
    }

    h1 {
      font-size: 2.2rem;
      color: #312e81;
      margin-bottom: 12px;
      text-shadow: 1px 1px 2px rgba(0,0,0,0.1);
    }

    h2 {
      font-size: 1.5rem;
      color: var(--primary);
      margin-bottom: 16px;
    }

    p.subtitle {
      font-size: 1.05rem;
      color: var(--text-muted);
      margin-bottom: 20px;
      max-width: 600px;
    }

    .input-group {
      margin: 20px 0;
      width: 100%;
      max-width: 360px;
    }

    input[type="text"] {
      width: 100%;
      padding: 14px 20px;
      border: 2px solid #cbd5e1;
      border-radius: 14px;
      font-size: 1.1rem;
      outline: none;
      text-align: center;
      transition: all 0.3s;
    }

    input[type="text"]:focus {
      border-color: var(--primary);
      box-shadow: 0 0 0 4px rgba(79, 70, 229, 0.2);
    }

    .btn {
      background: var(--primary);
      color: white;
      border: none;
      padding: 14px 32px;
      font-size: 1.1rem;
      font-weight: 700;
      border-radius: 14px;
      cursor: pointer;
      transition: all 0.2s;
      box-shadow: 0 6px 16px rgba(79, 70, 229, 0.3);
      margin: 8px;
    }

    .btn:hover {
      background: var(--primary-hover);
      transform: translateY(-2px);
      box-shadow: 0 8px 20px rgba(79, 70, 229, 0.4);
    }

    .btn:active {
      transform: translateY(0);
    }

    .btn-secondary {
      background: #64748b;
      box-shadow: 0 6px 16px rgba(100, 116, 139, 0.3);
    }
    .btn-secondary:hover { background: #475569; }

    /* Rules Modal */
    .modal {
      display: none;
      position: fixed;
      top: 0; left: 0; width: 100%; height: 100%;
      background: rgba(0,0,0,0.6);
      z-index: 100;
      justify-content: center;
      align-items: center;
      padding: 16px;
    }

    .modal-content {
      background: white;
      padding: 28px;
      border-radius: 20px;
      max-width: 550px;
      width: 100%;
      text-align: left;
      box-shadow: 0 10px 30px rgba(0,0,0,0.3);
    }

    .modal-content h3 {
      color: var(--primary);
      margin-bottom: 12px;
      font-size: 1.4rem;
    }

    .modal-content ul {
      margin-left: 20px;
      margin-bottom: 20px;
      line-height: 1.6;
    }

    /* Options Grid */
    .options-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
      gap: 12px;
      width: 100%;
      max-width: 650px;
      margin: 20px 0;
    }

    .opt-btn {
      background: #f8fafc;
      border: 2px solid #e2e8f0;
      padding: 16px 12px;
      border-radius: 14px;
      font-size: 1.05rem;
      font-weight: 600;
      color: #334155;
      cursor: pointer;
      transition: all 0.2s;
    }

    .opt-btn:hover:not(:disabled) {
      border-color: var(--primary);
      background: #eef2ff;
      transform: translateY(-2px);
    }

    .opt-btn.correct {
      background: #dcfce7 !important;
      border-color: var(--success) !important;
      color: #15803d !important;
    }

    .opt-btn.wrong {
      background: #fee2e2 !important;
      border-color: var(--danger) !important;
      color: #b91c1c !important;
    }

    /* Question Box */
    .question-card {
      background: #f1f5f9;
      border-left: 6px solid var(--primary);
      padding: 20px;
      border-radius: 14px;
      width: 100%;
      max-width: 650px;
      margin-bottom: 20px;
      font-size: 1.3rem;
      font-weight: 700;
      color: #1e293b;
    }

    /* Feedback Box */
    .feedback {
      min-height: 50px;
      font-size: 1.1rem;
      font-weight: 700;
      margin-top: 10px;
      display: flex;
      align-items: center;
      justify-content: center;
      border-radius: 10px;
      padding: 10px;
      width: 100%;
      max-width: 650px;
    }
    .feedback.correct-text { color: var(--success); background: #f0fdf4; }
    .feedback.wrong-text { color: var(--danger); background: #fef2f2; }

    /* Level 2: Matching layout */
    .matching-container {
      display: flex;
      justify-content: space-between;
      gap: 20px;
      width: 100%;
      max-width: 650px;
      margin: 16px 0;
    }
    .match-col {
      flex: 1;
      display: flex;
      flex-direction: column;
      gap: 10px;
    }
    .match-item {
      padding: 14px;
      background: #f8fafc;
      border: 2px solid #cbd5e1;
      border-radius: 12px;
      cursor: pointer;
      font-weight: 600;
      transition: all 0.2s;
    }
    .match-item.selected {
      border-color: var(--accent);
      background: #fef3c7;
    }
    .match-item.matched {
      background: #dcfce7;
      border-color: var(--success);
      color: #15803d;
      cursor: default;
      opacity: 0.8;
    }

    /* Level 4: Sentence Analysis */
    .sentence-container {
      display: flex;
      flex-wrap: wrap;
      gap: 10px;
      justify-content: center;
      margin: 20px 0;
      background: #f8fafc;
      padding: 20px;
      border-radius: 16px;
      border: 2px dashed #cbd5e1;
    }

    .word-token {
      background: white;
      border: 2px solid #94a3b8;
      padding: 10px 16px;
      border-radius: 10px;
      font-weight: 700;
      cursor: pointer;
      transition: all 0.2s;
    }
    .word-token.selected {
      border-color: var(--primary);
      background: #eef2ff;
      color: var(--primary);
    }
    .word-token.tagged {
      border-color: var(--success);
      background: #dcfce7;
      color: #15803d;
    }

    .tag-badge {
      display: block;
      font-size: 0.75rem;
      color: #475569;
      margin-top: 4px;
    }

    /* Certificate / End Screen */
    .certificate {
      background: radial-gradient(circle, #ffffff 0%, #f1f5f9 100%);
      border: 6px double var(--primary);
      border-radius: 20px;
      padding: 30px;
      width: 100%;
      max-width: 650px;
      box-shadow: 0 10px 25px rgba(0,0,0,0.1);
      margin-bottom: 20px;
    }

    .cert-title {
      font-size: 2rem;
      color: #312e81;
      font-weight: 900;
    }

    .cert-name {
      font-size: 1.8rem;
      color: var(--accent);
      text-decoration: underline;
      margin: 12px 0;
    }

    .cert-badge {
      font-size: 1.4rem;
      font-weight: 800;
      margin: 16px 0;
      padding: 10px 20px;
      border-radius: 50px;
      display: inline-block;
    }
    .badge-alo { background: #dcfce7; color: #166534; }
    .badge-yaxshi { background: #dbeafe; color: #1e40af; }
    .badge-harakat { background: #fef3c7; color: #9a3412; }

    /* Progress bar */
    .progress-bar-wrap {
      width: 100%;
      height: 10px;
      background: #e2e8f0;
      border-radius: 5px;
      overflow: hidden;
      margin-top: 10px;
    }
    .progress-bar {
      height: 100%;
      width: 0%;
      background: var(--primary);
      transition: width 0.3s;
    }

    /* Responsive design adjustments */
    @media (max-width: 600px) {
      .game-container { padding: 16px; min-height: 520px; }
      h1 { font-size: 1.6rem; }
      h2 { font-size: 1.2rem; }
      .question-card { font-size: 1.1rem; padding: 14px; }
      .btn { padding: 12px 24px; font-size: 1rem; }
      .matching-container { flex-direction: column; }
    }
  </style>
</head>
<body>

  <div class="game-container">
    <div class="bg-bubble bubble-1"></div>
    <div class="bg-bubble bubble-2"></div>

    <!-- Header bar -->
    <header id="game-header" style="display: none;">
      <div class="player-info">👤 <span id="display-player-name">O‘quvchi</span></div>
      <div style="font-weight:700; color:var(--primary);" id="level-indicator">1-bosqich</div>
      <div class="score-badge">⭐ <span id="display-score">0</span> ball</div>
    </header>

    <!-- PROGRESS BAR -->
    <div class="progress-bar-wrap" id="progress-wrap" style="display: none;">
      <div class="progress-bar" id="progress-bar"></div>
    </div>

    <!-- HOME SCREEN -->
    <div id="screen-home" class="screen active">
      <h1>🚀 So‘z turkumlari olamiga sayohat</h1>
      <p class="subtitle">Ona tili fanidan bilimingizni sinab ko‘ring! 5 ta qiziqarli bosqichni bosib o‘ting va haqiqiy bilimdonga aylaning!</p>
      
      <div class="input-group">
        <input type="text" id="player-name-input" placeholder="Ismingizni kiriting..." maxlength="20">
      </div>

      <div>
        <button class="btn" onclick="startGame()">O‘yinni boshlash 🎮</button>
        <button class="btn btn-secondary" onclick="toggleRules(true)">Qoidalar 📜</button>
      </div>
    </div>

    <!-- LEVEL 1: TOP! -->
    <div id="screen-level1" class="screen">
      <h2>1-bosqich: «So‘z turkumini top!» 🎯</h2>
      <p class="subtitle">Berilgan so‘z qaysi so‘z turkumiga tegishli ekanini aniqlang.</p>
      <div class="question-card" id="l1-word">...</div>
      <div class="options-grid" id="l1-options"></div>
      <div class="feedback" id="l1-feedback"></div>
    </div>

    <!-- LEVEL 2: JUFTINI TOP! -->
    <div id="screen-level2" class="screen">
      <h2>2-bosqich: «Juftini top!» 🔗</h2>
      <p class="subtitle">So‘zlar va ularning so‘roqlarini to‘g‘ri moslashtiring! (Chapdan va o‘ngdan juftini tanlang)</p>
      <div class="matching-container">
        <div class="match-col" id="l2-left"></div>
        <div class="match-col" id="l2-right"></div>
      </div>
      <div class="feedback" id="l2-feedback"></div>
      <button class="btn" id="l2-next-btn" style="display:none;" onclick="nextLevel()">Keyingi bosqich ➡️</button>
    </div>

    <!-- LEVEL 3: ORTIQCHASINI ANIQLANG! -->
    <div id="screen-level3" class="screen">
      <h2>3-bosqich: «Ortiqchasini aniqlang!» 🔍</h2>
      <p class="subtitle">Berilgan 4 ta so‘z orasidan boshqa so‘z turkumiga tegishli ortiqcha so‘zni toping!</p>
      <div class="question-card" id="l3-prompt">Boshqa so‘z turkumiga tegishlisini tanlang:</div>
      <div class="options-grid" id="l3-options"></div>
      <div class="feedback" id="l3-feedback"></div>
    </div>

    <!-- LEVEL 4: GAPNI TAHLIL QIL! -->
    <div id="screen-level4" class="screen">
      <h2>4-bosqich: «Gapni tahlil qil!» 📝</h2>
      <p class="subtitle">Gapdagi har bir so‘z ustiga bosing va uning so‘z turkumini tanlang!</p>
      <div class="sentence-container" id="l4-sentence"></div>
      <div style="font-weight:bold; margin-bottom:10px; color:#475569;" id="l4-target-word">Tanlangan so‘z: -</div>
      <div class="options-grid" id="l4-options"></div>
      <div class="feedback" id="l4-feedback"></div>
      <button class="btn" id="l4-next-btn" style="display:none;" onclick="nextLevel()">Keyingi bosqich ➡️</button>
    </div>

    <!-- LEVEL 5: BILIMDONLAR BELLASHUVI -->
    <div id="screen-level5" class="screen">
      <h2>5-bosqich: «Bilimdonlar bellashuvi» 🏆</h2>
      <p class="subtitle">Murakkab test savollariga javob bering!</p>
      <div class="question-card" id="l5-question">...</div>
      <div class="options-grid" id="l5-options"></div>
      <div class="feedback" id="l5-feedback"></div>
    </div>

    <!-- END SCREEN / RESULT -->
    <div id="screen-end" class="screen">
      <div class="certificate">
        <div class="cert-title">SERTIFIKAT</div>
        <p>«So‘z turkumlari olamiga sayohat» o‘yini yakunlandi!</p>
        <div class="cert-name" id="end-player-name">Bilimdon</div>
        <p style="font-size:1.2rem; font-weight:700;">To‘plangan umumiy ball: <span id="end-score" style="color:var(--primary); font-size:1.5rem;">0</span> / <span id="max-score">0</span></p>
        <div class="cert-badge" id="end-badge">A’lo!</div>
        <p id="end-message" style="color:var(--text-muted); font-size:1.05rem; line-height:1.5;">Barakalla!</p>
      </div>

      <div>
        <button class="btn" onclick="restartGame()">🔄 Qayta o‘ynash</button>
      </div>
    </div>

  </div>

  <!-- RULES MODAL -->
  <div class="modal" id="rules-modal">
    <div class="modal-content">
      <h3>📜 O‘yin qoidalari</h3>
      <ul>
        <li>O‘yin 5 ta sinov bosqichidan iborat.</li>
        <li>Har bir to‘g‘ri javob uchun <strong>10 ball</strong> beriladi.</li>
        <li><strong>1-bosqich:</strong> So‘zning qaysi turkumligini toping (10 ta savol).</li>
        <li><strong>2-bosqich:</strong> So‘z va uning so‘rog‘i/turkumini juftlang.</li>
        <li><strong>3-bosqich:</strong> 4 ta so‘z orasidan turkumi boshqacha bo‘lgan ortiqchasini toping.</li>
        <li><strong>4-bosqich:</strong> Gapdagi har bir so‘zning turkumini aniqlang.</li>
        <li><strong>5-bosqich:</strong> 10 ta test savoliga to‘g‘ri javob tanlang.</li>
        <li>O‘yin yakunida umumiy ballingiz va darajangiz ko‘rsatiladi. Omad!</li>
      </ul>
      <div style="text-align: right;">
        <button class="btn" onclick="toggleRules(false)">Tushundim 👍</button>
      </div>
    </div>
  </div>

  <script>
    // --- AUDIO SYNTHESIZER (No external audio files required) ---
    const audioCtx = new (window.AudioContext || window.webkitAudioContext)();
    function playSound(type) {
      if (audioCtx.state === 'suspended') audioCtx.resume();
      const osc = audioCtx.createOscillator();
      const gain = audioCtx.createGain();
      osc.connect(gain);
      gain.connect(audioCtx.destination);

      if (type === 'correct') {
        osc.type = 'sine';
        osc.frequency.setValueAtTime(523.25, audioCtx.currentTime); // C5
        osc.frequency.exponentialRampToValueAtTime(659.25, audioCtx.currentTime + 0.15); // E5
        gain.gain.setValueAtTime(0.3, audioCtx.currentTime);
        gain.gain.exponentialRampToValueAtTime(0.01, audioCtx.currentTime + 0.3);
        osc.start(); osc.stop(audioCtx.currentTime + 0.3);
      } else if (type === 'wrong') {
        osc.type = 'sawtooth';
        osc.frequency.setValueAtTime(220, audioCtx.currentTime); // A3
        osc.frequency.exponentialRampToValueAtTime(140, audioCtx.currentTime + 0.25);
        gain.gain.setValueAtTime(0.3, audioCtx.currentTime);
        gain.gain.exponentialRampToValueAtTime(0.01, audioCtx.currentTime + 0.3);
        osc.start(); osc.stop(audioCtx.currentTime + 0.3);
      } else if (type === 'win') {
        osc.type = 'triangle';
        osc.frequency.setValueAtTime(440, audioCtx.currentTime);
        osc.frequency.exponentialRampToValueAtTime(880, audioCtx.currentTime + 0.4);
        gain.gain.setValueAtTime(0.3, audioCtx.currentTime);
        gain.gain.exponentialRampToValueAtTime(0.01, audioCtx.currentTime + 0.5);
        osc.start(); osc.stop(audioCtx.currentTime + 0.5);
      }
    }

    // --- GAME DATA ---
    const TURKUMLAR = ["Ot", "Sifat", "Son", "Olmosh", "Fe’l", "Ravish"];

    // Level 1: 10 Words
    const level1Data = [
      { word: "Maktab", correct: "Ot" },
      { word: "Zukko", correct: "Sifat" },
      { word: "O‘n yetti", correct: "Son" },
      { word: "Ular", correct: "Olmosh" },
      { word: "Yozmoqda", correct: "Fe’l" },
      { word: "Tezda", correct: "Ravish" },
      { word: "Kitob", correct: "Ot" },
      { word: "Chiroyli", correct: "Sifat" },
      { word: "Mening", correct: "Olmosh" },
      { word: "Kulyapti", correct: "Fe’l" }
    ];

    // Level 2: Pairs
    const level2Pairs = [
      { id: 1, left: "Kitob", right: "Nima? (Ot)" },
      { id: 2, left: "Shirin", right: "Qanday? (Sifat)" },
      { id: 3, left: "Besh", right: "Nechta? (Son)" },
      { id: 4, left: "Biz", right: "Kimlar? (Olmosh)" },
      { id: 5, left: "Sakradi", right: "Nima qildi? (Fe’l)" },
      { id: 6, left: "Hozir", right: "Qachon? (Ravish)" }
    ];

    // Level 3: Odd One Out (5 Rounds)
    const level3Data = [
      { words: ["Qalam", "Daftar", "Kitob", "O‘qidi"], odd: "O‘qidi", reason: "O‘qidi - Fe’l (boshqalari Ot)" },
      { words: ["Katta", "Baland", "Chiroyli", "Shahar"], odd: "Shahar", reason: "Shahar - Ot (boshqalari Sifat)" },
      { words: ["Bir", "O‘n", "Yetti", "Ular"], odd: "Ular", reason: "Ular - Olmosh (boshqalari Son)" },
      { words: ["Yozdi", "Chizdi", "Kuyladi", "Sehrli"], odd: "Sehrli", reason: "Sehrli - Sifat (boshqalari Fe’l)" },
      { words: ["Tezda", "Bugun", "Sekin", "Olma"], odd: "Olma", reason: "Olma - Ot (boshqalari Ravish)" }
    ];

    // Level 4: Sentence Breakdown (5 Sentences)
    const level4Data = [
      {
        tokens: [
          { word: "Zukko", turkum: "Sifat" },
          { word: "o‘quvchi", turkum: "Ot" },
          { word: "kitobni", turkum: "Ot" },
          { word: "tezda", turkum: "Ravish" },
          { word: "o‘qidi.", turkum: "Fe’l" }
        ]
      },
      {
        tokens: [
          { word: "Biz", turkum: "Olmosh" },
          { word: "chiroyli", turkum: "Sifat" },
          { word: "bog‘da", turkum: "Ot" },
          { word: "o‘ynadik.", turkum: "Fe’l" }
        ]
      },
      {
        tokens: [
          { word: "Besh", turkum: "Son" },
          { word: "bola", turkum: "Ot" },
          { word: "baland", turkum: "Sifat" },
          { word: "tog‘ga", turkum: "Ot" },
          { word: "chiqdi.", turkum: "Fe’l" }
        ]
      }
    ];

    // Level 5: Test (10 Questions)
    const level5Data = [
      {
        q: "Ot turkumiga oid so‘zlar qaysi so‘roqlarga javob bo‘ladi?",
        opts: ["Kim? Nima? Qayer?", "Qanday? Qanaqa?", "Nechta? Nechanchi?", "Nima qildi? Nima qilyapti?"],
        ans: 0
    #Url yaratish

Click.uz saytiga yuborish uchun biza url yaratishmiza kerak
bu url klientga korsatiladi va urlga kirganida klient pul tolash qismiga otib ketadi

![alt text](https://i.imgur.com/AnX0wSd.png)
```python
from clickuz import ClickUz

url = ClickUz.generate_url(order_id='172',amount='150000')
print(url)
```

!!! return_url
    Agar klient pul tolab bolganidan keyn saytga qaytib kelishini xoxlasangiz
    *return_url* ga ozingizni domain qoshib qoyishiz kerak boladi

```python
from clickuz import ClickUz

url = ClickUz.generate_url(order_id='172',amount='150000',return_url='http://example.com')
print(url)
```
Klient pul tolab bolganidan keyn sizning saytizga qaytib keladi
