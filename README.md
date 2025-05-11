<!DOCTYPE html>
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
  </style>
</head>
<body>
  <h1 id="title">Надад болзоонд явах уу? 💌</h1>
  <div class="button-group" id="invite">
    <button onclick="startQuestions()">Тийм</button>
    <button onclick="decline()">Үгүй</button>
  </div>

  <div id="q1" class="container">
    <h2>1. Ямар хоолонд дуртай вэ?</h2>
    <button onclick="nextQuestion(1, 'Итали')">Итали</button>
    <button onclick="nextQuestion(1, 'Япон')">Япон</button>
    <button onclick="nextQuestion(1, 'Монгол')">Монгол</button>
  </div>

  <div id="q2" class="container">
    <h2>2. Болзоогоо хаана хиймээр байна?</h2>
    <button onclick="nextQuestion(2, 'Кафе')">Кафе</button>
    <button onclick="nextQuestion(2, 'Кино театр')">Кино театр</button>
    <button onclick="nextQuestion(2, 'Гадаа алхах')">Гадаа алхах</button>
  </div>

  <div id="q3" class="container">
    <h2>3. Гэнэтийн бэлгэнд дуртай юу?</h2>
    <button onclick="nextQuestion(3, 'Тийм')">Тийм</button>
    <button onclick="nextQuestion(3, 'Үгүй')">Үгүй</button>
  </div>

  <div id="q4" class="container">
    <h2>4. Чи намайг хөөрхөн гэж боддог уу? 😳</h2>
    <button onclick="nextQuestion(4, 'Мэдээж!')">Мэдээж!</button>
    <button onclick="nextQuestion(4, 'Хөөрхөн бас хөөрхөн 😄')">Хөөрхөн бас хөөрхөн 😄</button>
  </div>

  <div id="summary" class="container">
    <h2>💘 Болзооны хариултууд:</h2>
    <p id="a1"></p>
    <p id="a2"></p>
    <p id="a3"></p>
    <p id="a4"></p>
  </div>

  <script>
    let answers = {};

    function startQuestions() {
      document.getElementById("title").style.display = "none";
      document.getElementById("invite").style.display = "none";
      document.getElementById("q1").classList.add("active");
    }

    function decline() {
      document.getElementById("title").textContent = "Харамсалтай байна 😢";
      document.getElementById("invite").style.display = "none";
    }

    function nextQuestion(num, answer) {
      answers[`q${num}`] = answer;
      document.getElementById(`q${num}`).classList.remove("active");
      if (num < 4) {
        document.getElementById(`q${num + 1}`).classList.add("active");
      } else {
        showSummary();
      }
    }

    function showSummary() {
      document.getElementById("summary").style.display = "block";
      document.getElementById("a1").textContent = `1. Дуртай хоол: ${answers.q1}`;
      document.getElementById("a2").textContent = `2. Болзооны газар: ${answers.q2}`;
      document.getElementById("a3").textContent = `3. Гэнэтийн бэлэг: ${answers.q3}`;
      document.getElementById("a4").textContent = `4. Миний тухай бодол: ${answers.q4}`;
    }

    // Сайхан зүрхнүүд
    for (let i = 0; i < 30; i++) {
      const heart = document.createElement('div');
      heart.className = 'heart';
      heart.style.left = Math.random() * 100 + 'vw';
      heart.style.animationDuration = (2 + Math.random() * 4) + 's';
      document.body.appendChild(heart);
    }
  </script>
</body>
</html>
