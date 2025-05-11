<html lang="mn">
<head>
  <meta charset="UTF-8">
  <title>Болзооны урилга 💖</title>
  <style>
    body {
      font-family: 'Segoe UI', sans-serif;
      background: linear-gradient(to bottom, #ffe6f0, #ffd1e8);
      text-align: center;
      color: #d6336c;
      overflow: hidden;
      margin: 0;
      padding: 0;
    }

    h1 {
      margin-top: 60px;
      font-size: 2.5rem;
      animation: pulse 1.2s infinite alternate;
    }

    @keyframes pulse {
      from { transform: scale(1); }
      to { transform: scale(1.05); }
    }

    .container {
      display: none;
      padding: 30px;
      animation: fadeIn 0.5s ease;
    }

    .container.active {
      display: block;
    }

    @keyframes fadeIn {
      from { opacity: 0; transform: translateX(50px); }
      to { opacity: 1; transform: translateX(0); }
    }

    .button-group {
      margin-top: 30px;
    }

    button {
      margin: 12px;
      padding: 12px 24px;
      font-size: 1.2rem;
      background-color: #ff4081;
      color: white;
      border: none;
      border-radius: 10px;
      cursor: pointer;
      transition: transform 0.2s, background 0.3s;
    }

    button:hover {
      background-color: #c2185b;
      transform: scale(1.05);
    }

    .heart {
      position: fixed;
      width: 20px;
      height: 20px;
      background: red;
      transform: rotate(45deg);
      animation: float 6s linear infinite;
      opacity: 0.5;
      z-index: -1;
    }

    .heart::before, .heart::after {
      content: '';
      position: absolute;
      width: 20px;
      height: 20px;
      background: red;
      border-radius: 50%;
    }

    .heart::before {
      top: -10px;
      left: 0;
    }

    .heart::after {
      top: 0;
      left: -10px;
    }

    @keyframes float {
      0% { transform: translateY(0) rotate(45deg); }
      100% { transform: translateY(-100vh) rotate(45deg); }
    }

    #summary {
      font-size: 1.3rem;
      margin-top: 30px;
      display: none;
    }

    textarea {
      width: 80%;
      height: 100px;
      margin-top: 20px;
      padding: 10px;
      border-radius: 8px;
      border: 1px solid #ccc;
      font-size: 1rem;
    }

    .sparkle {
      position: fixed;
      width: 10px;
      height: 10px;
      background: radial-gradient(white, transparent);
      border-radius: 50%;
      opacity: 0.6;
      animation: sparkle 5s linear infinite;
      pointer-events: none;
      z-index: -1;
    }

    @keyframes sparkle {
      0% {
        transform: translateY(0) scale(1);
        opacity: 0.8;
      }
      100% {
        transform: translateY(-100vh) scale(0.5);
        opacity: 0;
      }
    }
  </style>
</head>
<body>
  <h1 id="title">Надтай болзоонд явах уу, Номио? 💌</h1>
  <div class="button-group" id="invite">
    <button onclick="startQuestions()">Тийм</button>
    <button onclick="forceYes()">Үгүй</button>
  </div>

  <div id="q1" class="container">
    <h2>1. Ямар хоолонд дуртай вэ?</h2>
    <button onclick="nextQuestion(1, 'Хятад')">Хятад</button>
    <button onclick="nextQuestion(1, 'Япон')">Япон</button>
    <button onclick="nextQuestion(1, 'Монгол')">Монгол</button>
  </div>

  <div id="q2" class="container">
    <h2>2. Болзоогоо хаана хиймээр байна?</h2>
    <button onclick="nextQuestion(2, 'Кафе')">Кафе</button>
    <button onclick="nextQuestion(2, 'Кино театр')">Кино театр</button>
    <button onclick="nextQuestion(2, 'Гадаа алхах')">Гадаа алхах</button>
    <button onclick="nextQuestion(2, 'Бүгд')">Бүгд</button>
  </div>

  <div id="q3" class="container">
    <h2>3. Гэнэтийн бэлгэнд дуртай юу?</h2>
    <button onclick="nextQuestion(3, 'Тийм')">Тийм</button>
    <button onclick="nextQuestion(3, 'Үгүй')">Үгүй</button>
  </div>

  <div id="q4" class="container">
    <h2>4. Болзооны үеэр өөр ямар сонирхолтой зүйл хийх вэ?</h2>
    <textarea id="input-q4" placeholder="Санаагаа энд бичнэ үү..."></textarea><br>
    <button onclick="nextTextAnswer(4)">Дараах</button>
  </div>

  <div id="q5" class="container">
    <h2>5. Болзоо хэзээ вэ? 📅</h2>
    <button onclick="nextQuestion(5, 'Хагас сайн')">Хагас сайн</button>
    <button onclick="nextQuestion(5, 'Бүтэн сайн')">Бүтэн сайн</button>
  </div>

  <div id="summary" class="container">
    <h2>💘 Хүлээж тэсэхгүй нь!</h2>
    <p id="a1"></p>
    <p id="a2"></p>
    <p id="a3"></p>
    <p id="a4"></p>
    <p id="a5"></p>
  </div>

  <script>
    let answers = {};

    function startQuestions() {
      document.getElementById("title").style.display = "none";
      document.getElementById("invite").style.display = "none";
      document.getElementById("q1").classList.add("active");
    }

    function forceYes() {
      alert("Буруу дарсан юм шиг байна, Тийм гэж ойлголоо! 😄");
      startQuestions();
    }

    function nextQuestion(num, answer) {
      answers[`q${num}`] = answer;
      document.getElementById(`q${num}`).classList.remove("active");
      if (num < 5) {
        document.getElementById(`q${num + 1}`).classList.add("active");
      } else {
        showSummary();
      }
    }

    function nextTextAnswer(num) {
      const value = document.getElementById("input-q4").value.trim();
      answers[`q${num}`] = value || "Хоосон";
      document.getElementById(`q${num}`).classList.remove("active");
      document.getElementById("q5").classList.add("active");
    }

    function showSummary() {
      document.getElementById("summary").style.display = "block";
      document.getElementById("a1").textContent = `1. Дуртай хоол: ${answers.q1}`;
      document.getElementById("a2").textContent = `2. Болзооны газар: ${answers.q2}`;
      document.getElementById("a3").textContent = `3. Гэнэтийн бэлэг: ${answers.q3}`;
      document.getElementById("a4").textContent = `4. Санал: ${answers.q4}`;
      document.getElementById("a5").textContent = `5. Болзоо хэзээ: ${answers.q5}`;
    }

    // Зүрхнүүд
    for (let i = 0; i < 30; i++) {
      const heart = document.createElement('div');
      heart.className = 'heart';
      heart.style.left = Math.random() * 100 + 'vw';
      heart.style.animationDuration = (2 + Math.random() * 4) + 's';
      document.body.appendChild(heart);
    }

    // Гялтганасан од
    for (let i = 0; i < 40; i++) {
      const sparkle = document.createElement('div');
      sparkle.className = 'sparkle';
      sparkle.style.left = Math.random() * 100 + 'vw';
      sparkle.style.animationDuration = (3 + Math.random() * 3) + 's';
      sparkle.style.animationDelay = Math.random() * 5 + 's';
      document.body.appendChild(sparkle);
    }
  </script>
</body>
</html>
