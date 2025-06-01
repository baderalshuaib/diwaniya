# diwaniya
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Trivia Game - Home</title>
  <link rel="stylesheet" href="style.css" />
</head>
<body class="dark">
  <header>
    <h1>Trivia Game</h1>
    <nav>
      <a href="index.html">Home</a>
      <a href="about.html">About</a>
      <a href="faq.html">FAQ</a>
      <a href="contact.html">Contact</a>
    </nav>
  </header>

  <main>
    <section class="welcome">
      <h2>Welcome to the Trivia Game!</h2>
      <p>Test your knowledge and climb the leaderboard.</p>

      <div class="auth-box">
        <input type="text" id="username" placeholder="Enter your username" />
        <button onclick="login()">Login / Register</button>
      </div>

      <button class="start-btn" onclick="startQuiz()">Start Quiz</button>
    </section>
  </main>

  <footer>
    <p>&copy; 2025 Trivia Game. All rights reserved.</p>
  </footer>

  <script src="script.js"></script>
</body>
</html>
body.dark {
  background-color: #121212;
  color: #f0f0f0;
  font-family: Arial, sans-serif;
  margin: 0;
  padding: 0;
}

header {
  background: #1e1e1e;
  padding: 15px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

nav a {
  margin: 0 10px;
  color: #bbb;
  text-decoration: none;
}

nav a:hover {
  color: #fff;
}

main {
  padding: 40px;
  text-align: center;
}

.auth-box {
  margin: 20px 0;
}

input[type="text"] {
  padding: 10px;
  width: 200px;
  border: none;
  border-radius: 4px;
}

.start-btn, .auth-box button {
  padding: 10px 20px;
  margin-top: 10px;
  background-color: #333;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.start-btn:hover, .auth-box button:hover {
  background-color: #555;
}

footer {
  background: #1e1e1e;
  text-align: center;
  padding: 15px;
}
function login() {
  const username = document.getElementById("username").value.trim();
  if (username) {
    localStorage.setItem("trivia_user", username);
    alert("Welcome, " + username + "!");
  } else {
    alert("Please enter a username.");
  }
}

function startQuiz() {
  const user = localStorage.getItem("trivia_user");
  if (!user) {
    alert("Please log in first.");
    return;
  }
  window.location.href = "quiz.html"; // We'll build this next
}
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Trivia Quiz</title>
  <link rel="stylesheet" href="style.css" />
</head>
<body class="dark">
  <header>
    <h1>Trivia Quiz</h1>
    <nav>
      <a href="index.html">Home</a>
      <a href="about.html">About</a>
      <a href="faq.html">FAQ</a>
      <a href="contact.html">Contact</a>
    </nav>
  </header>

  <main>
    <div class="quiz-container" id="quiz-box">
      <h2 id="question">Loading...</h2>
      <div id="options"></div>
      <button onclick="nextQuestion()">Next</button>
    </div>
    <div id="result" style="display: none;">
      <h2>Quiz Completed!</h2>
      <p id="score-text"></p>
      <a href="index.html"><button>Back to Home</button></a>
    </div>
  </main>

  <script src="quiz.js"></script>
</body>
</html>
const questions = [
  {
    question: "What is the capital of France?",
    options: ["Berlin", "Paris", "Madrid", "Rome"],
    answer: "Paris"
  },
  {
    question: "Which planet is known as the Red Planet?",
    options: ["Venus", "Mars", "Jupiter", "Saturn"],
    answer: "Mars"
  },
  {
    question: "What is the largest mammal?",
    options: ["Elephant", "Blue Whale", "Shark", "Giraffe"],
    answer: "Blue Whale"
  }
];

let currentQuestion = 0;
let score = 0;

function loadQuestion() {
  const q = questions[currentQuestion];
  document.getElementById("question").textContent = q.question;

  const optionsDiv = document.getElementById("options");
  optionsDiv.innerHTML = "";
  q.options.forEach(option => {
    const btn = document.createElement("button");
    btn.textContent = option;
    btn.className = "option-btn";
    btn.onclick = () => checkAnswer(option);
    optionsDiv.appendChild(btn);
  });
}

function checkAnswer(selected) {
  const correct = questions[currentQuestion].answer;
  if (selected === correct) {
    score++;
  }
  Array.from(document.querySelectorAll(".option-btn")).forEach(btn => {
    btn.disabled = true;
    if (btn.textContent === correct) {
      btn.style.backgroundColor = "green";
    } else if (btn.textContent === selected) {
      btn.style.backgroundColor = "red";
    }
  });
}

function nextQuestion() {
  if (currentQuestion < questions.length - 1) {
    currentQuestion++;
    loadQuestion();
  } else {
    document.getElementById("quiz-box").style.display = "none";
    document.getElementById("result").style.display = "block";
    document.getElementById("score-text").textContent =
      `You scored ${score} out of ${questions.length}!`;
  }
}

window.onload = loadQuestion;
