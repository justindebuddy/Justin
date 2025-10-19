<html lang="zh">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Buddy Hunting Quiz</title>
  <style>
    body {
      font-family: "Segoe UI", sans-serif;
      background: linear-gradient(135deg, #ffe6f0, #d9e7ff);
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      margin: 0;
    }

    .container {
      background: white;
      border-radius: 20px;
      box-shadow: 0 8px 30px rgba(0, 0, 0, 0.15);
      width: 90%;
      max-width: 400px;
      text-align: center;
      padding: 30px;
      animation: fadeIn 1s ease;
    }

    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(20px); }
      to { opacity: 1; transform: translateY(0); }
    }

    h1 {
      font-size: 24px;
      color: #333;
    }

    .btn {
      background-color: #6ca0dc;
      color: white;
      border: none;
      border-radius: 10px;
      padding: 12px 24px;
      font-size: 16px;
      cursor: pointer;
      margin-top: 20px;
      transition: all 0.25s ease;
    }

    .btn:hover {
      background-color: #558acb;
      transform: scale(1.05);
    }

    .option {
      display: block;
      margin: 12px auto;
      padding: 12px 20px;
      width: 80%;
      border: none;
      border-radius: 10px;
      background-color: #f2f2f2;
      font-size: 16px;
      cursor: pointer;
      transition: all 0.25s ease;
    }

    .option:hover {
      background-color: #d0eaff;
      transform: scale(1.03);
    }

    .option.correct {
      background-color: #b9f6ca;
    }

    .option.wrong {
      background-color: #ffcdd2;
    }

    .message {
      margin-top: 20px;
      font-weight: bold;
      color: #444;
    }

    .hidden {
      display: none;
    }

    .final-message {
      font-size: 18px;
      color: #444;
      animation: pop 1s ease-in-out;
    }

    @keyframes pop {
      0% { transform: scale(0.8); opacity: 0; }
      100% { transform: scale(1); opacity: 1; }
    }
  </style>
</head>
<body>

  <div class="container" id="start-screen">
    <h1>🎯 欢迎来到 Buddy Hunting Quiz！</h1>
    <p>答对所有问题才能解锁你的线索哦～</p>
    <button class="btn" onclick="startQuiz()">开始答题</button>
  </div>

  <div class="container hidden" id="quiz-screen">
    <h1 id="question">Loading...</h1>
    <div id="options"></div>
    <div id="message" class="message"></div>
  </div>

  <script>
    const quiz = [
      {
        q: "蔡徐坤成名曲歌词里，唱，跳，rap 的下一句是什么？",
        options: ["篮球", "足球", "乒乓球"],
        answer: 0
      },
      {
        q: "鸡你太美的练习时长是多久？",
        options: ["两分半", "两年半", "凉拌"],
        answer: 1
      },
      {
        q: "你是蔡徐坤的真爱粉吗？",
        options: ["真爱粉", "小黑子"],
        answer: 0
      }
    ];

    let current = 0;

    const startScreen = document.getElementById("start-screen");
    const quizScreen = document.getElementById("quiz-screen");
    const questionEl = document.getElementById("question");
    const optionsEl = document.getElementById("options");
    const messageEl = document.getElementById("message");

    function startQuiz() {
      startScreen.classList.add("hidden");
      quizScreen.classList.remove("hidden");
      loadQuestion();
    }

    function loadQuestion() {
      const q = quiz[current];
      questionEl.textContent = q.q;
      optionsEl.innerHTML = "";
      messageEl.textContent = "";
      q.options.forEach((opt, i) => {
        const btn = document.createElement("button");
        btn.className = "option";
        btn.textContent = opt;
        btn.onclick = () => checkAnswer(i, btn);
        optionsEl.appendChild(btn);
      });
    }

    function checkAnswer(i, btn) {
      const correctIndex = quiz[current].answer;
      if (i === correctIndex) {
        btn.classList.add("correct");
        messageEl.textContent = "✅ 答对啦，你是真爱粉！";
        setTimeout(() => {
          current++;
          if (current < quiz.length) {
            loadQuestion();
          } else {
            showFinalMessage();
          }
        }, 1000);
      } else {
        btn.classList.add("wrong");
        messageEl.textContent = "❌ 小黑子！再试一次！";
      }
    }

    function showFinalMessage() {
      questionEl.textContent = "🎉 古有项羽无人敌,今有坤坤万人迷";
      optionsEl.innerHTML = `<div class="final-message">
        现在请到 <b>Dry Lab 外的 204 locker</b> 里获取你的线索！
      </div>`;
      messageEl.textContent = "";
    }
  </script>

</body>
</html>
