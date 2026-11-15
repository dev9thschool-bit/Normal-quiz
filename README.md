# Normal-quiz
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <title>Doraemon Quiz</title>

  <style>
    * {
      box-sizing: border-box;
    }

    body {
      margin: 0;
      font-family: Arial, sans-serif;
      background: #eaf7ff;
      color: #222;
    }

    .container {
      width: 92%;
      max-width: 700px;
      margin: 40px auto;
      background: white;
      padding: 25px;
      border-radius: 18px;
      box-shadow: 0 8px 25px rgba(0,0,0,0.12);
    }

    h1 {
      text-align: center;
      margin-bottom: 8px;
    }

    .subtitle {
      text-align: center;
      color: #666;
      margin-bottom: 25px;
    }

    input {
      width: 100%;
      padding: 14px;
      border: 1px solid #ccc;
      border-radius: 10px;
      font-size: 16px;
      margin: 10px 0 20px;
    }

    button {
      width: 100%;
      padding: 14px;
      border: none;
      border-radius: 10px;
      background: #168de2;
      color: white;
      font-size: 17px;
      cursor: pointer;
      margin-top: 10px;
    }

    button:hover {
      opacity: 0.9;
    }

    .hidden {
      display: none;
    }

    .progress {
      margin-bottom: 20px;
      color: #666;
      font-size: 14px;
    }

    .question {
      font-size: 20px;
      font-weight: bold;
      margin-bottom: 20px;
    }

    .option {
      display: block;
      width: 100%;
      padding: 14px;
      margin: 10px 0;
      border: 2px solid #ddd;
      border-radius: 10px;
      background: white;
      color: #222;
      text-align: left;
      cursor: pointer;
    }

    .option:hover {
      border-color: #168de2;
    }

    .option.selected {
      border-color: #168de2;
      background: #eaf6ff;
    }

    .result-score {
      text-align: center;
      font-size: 30px;
      font-weight: bold;
      margin: 20px 0;
    }

    .answer-review {
      margin-top: 25px;
    }

    .review-item {
      padding: 15px;
      border-radius: 10px;
      margin: 10px 0;
      background: #f5f5f5;
    }

    .correct {
      border-left: 5px solid green;
    }

    .wrong {
      border-left: 5px solid red;
    }

    .restart {
      margin-top: 20px;
    }
  </style>
</head>

<body>

  <div class="container">

    <!-- START SCREEN -->
    <div id="startScreen">

      <h1>🔵 Doraemon Quiz</h1>

      <p class="subtitle">
        How well do you know Doraemon?
      </p>

      <label for="playerName">Enter your name</label>

      <input
        type="text"
        id="playerName"
        placeholder="Your name"
        maxlength="40"
      >

      <button onclick="startQuiz()">
        Start Quiz
      </button>

    </div>


    <!-- QUIZ SCREEN -->
    <div id="quizScreen" class="hidden">

      <div class="progress" id="progress"></div>

      <div class="question" id="question"></div>

      <div id="options"></div>

      <button onclick="nextQuestion()" id="nextButton">
        Next
      </button>

    </div>


    <!-- RESULT SCREEN -->
    <div id="resultScreen" class="hidden">

      <h1>Quiz Complete!</h1>

      <p id="resultName"></p>

      <div class="result-score" id="score"></div>

      <p id="resultMessage"></p>

      <div class="answer-review">

        <h2>Your Answers</h2>

        <div id="review"></div>

      </div>

      <button class="restart" onclick="restartQuiz()">
        Try Again
      </button>

    </div>

  </div>


<script>

const questions = [

  {
    question: "What is Doraemon's favorite food?",
    options: [
      "Dorayaki",
      "Ramen",
      "Takoyaki",
      "Curry"
    ],
    answer: "Dorayaki"
  },

  {
    question: "Who is Doraemon's best friend?",
    options: [
      "Nobita",
      "Suneo",
      "Dekisugi",
      "Gian"
    ],
    answer: "Nobita"
  },

  {
    question: "What color is Doraemon?",
    options: [
      "Blue",
      "Green",
      "Purple",
      "Red"
    ],
    answer: "Blue"
  },

  {
    question: "Where did Doraemon originally come from?",
    options: [
      "The 22nd century",
      "The 25th century",
      "The 21st century",
      "The 30th century"
    ],
    answer: "The 22nd century"
  },

  {
    question: "What is the name of Nobita's dog?",
    options: [
      "Ichi",
      "Muku",
      "Koro",
      "Shiro"
    ],
    answer: "Muku"
  },

  {
    question: "Who often bullies Nobita?",
    options: [
      "Gian",
      "Dekisugi",
      "Sewashi",
      "Dorami"
    ],
    answer: "Gian"
  },

  {
    question: "Who is Nobita's smart classmate?",
    options: [
      "Dekisugi",
      "Suneo",
      "Gian",
      "Sewashi"
    ],
    answer: "Dekisugi"
  },

  {
    question: "What is Suneo especially known for?",
    options: [
      "Showing off his possessions",
      "Being very athletic",
      "Being extremely quiet",
      "Inventing gadgets"
    ],
    answer: "Showing off his possessions"
  },

  {
    question: "What is the Anywhere Door used for?",
    options: [
      "Traveling to different places",
      "Making food",
      "Becoming invisible",
      "Stopping time"
    ],
    answer: "Traveling to different places"
  },

  {
    question: "What does the Small Light do?",
    options: [
      "Makes objects smaller",
      "Makes objects invisible",
      "Makes objects fly",
      "Changes colors"
    ],
    answer: "Makes objects smaller"
  },

  {
    question: "What does the Big Light do?",
    options: [
      "Makes objects bigger",
      "Makes objects disappear",
      "Makes objects move faster",
      "Makes objects talk"
    ],
    answer: "Makes objects bigger"
  },

  {
    question: "What is Doraemon's sister called?",
    options: [
      "Dorami",
      "Dorama",
      "Dora",
      "Dori"
    ],
    answer: "Dorami"
  },

  {
    question: "What does Doraemon have instead of ears?",
    options: [
      "No ears",
      "Small antennas",
      "Metal ears",
      "Round ears"
    ],
    answer: "No ears"
  },

  {
    question: "Which gadget allows Nobita to fly?",
    options: [
      "Take-copter",
      "Anywhere Door",
      "Time Machine",
      "Small Light"
    ],
    answer: "Take-copter"
  },

  {
    question: "Where is the Take-copter usually placed?",
    options: [
      "On the head",
      "On the hand",
      "On the foot",
      "On the shoulder"
    ],
    answer: "On the head"
  },

  {
    question: "What does the Time Machine allow them to do?",
    options: [
      "Travel through time",
      "Become invisible",
      "Change size",
      "Read minds"
    ],
    answer: "Travel through time"
  },

  {
    question: "Who is Nobita's mother?",
    options: [
      "Tamako",
      "Shizuka",
      "Dorami",
      "Mii"
    ],
    answer: "Tamako"
  },

  {
    question: "Who does Nobita have a crush on?",
    options: [
      "Shizuka",
      "Dorami",
      "Tamako",
      "Jaiko"
    ],
    answer: "Shizuka"
  },

  {
    question: "What is the Time Furoshiki mainly associated with?",
    options: [
      "Changing an object's age or condition",
      "Flying",
      "Making food",
      "Teleporting"
    ],
    answer: "Changing an object's age or condition"
  },

  {
    question: "What is Doraemon's pocket called?",
    options: [
      "4D Pocket",
      "Magic Pocket",
      "Future Pocket",
      "Gadget Pocket"
    ],
    answer: "4D Pocket"
  }

];


let currentQuestion = 0;
let userAnswers = [];
let playerName = "";


/* Shuffle an array */
function shuffle(array) {

  let shuffled = [...array];

  for (let i = shuffled.length - 1; i > 0; i--) {

    const j = Math.floor(Math.random() * (i + 1));

    [shuffled[i], shuffled[j]] =
      [shuffled[j], shuffled[i]];
  }

  return shuffled;
}


/* Start quiz */
function startQuiz() {

  const nameInput =
    document.getElementById("playerName");

  playerName =
    nameInput.value.trim();

  if (!playerName) {

    alert("Please enter your name first.");

    return;
  }

  currentQuestion = 0;
  userAnswers = [];

  document
    .getElementById("startScreen")
    .classList.add("hidden");

  document
    .getElementById("resultScreen")
    .classList.add("hidden");

  document
    .getElementById("quizScreen")
    .classList.remove("hidden");

  showQuestion();
}


/* Display question */
function showQuestion() {

  const question =
    questions[currentQuestion];

  document.getElementById("progress").textContent =
    `Question ${currentQuestion + 1} of ${questions.length}`;

  document.getElementById("question").textContent =
    question.question;

  const optionsContainer =
    document.getElementById("options");

  optionsContainer.innerHTML = "";

  const shuffledOptions =
    shuffle(question.options);

  shuffledOptions.forEach(option => {

    const button =
      document.createElement("button");

    button.className = "option";

    button.textContent = option;

    button.onclick = function() {

      document
        .querySelectorAll(".option")
        .forEach(btn =>
          btn.classList.remove("selected")
        );

      button.classList.add("selected");

      button.dataset.selected = "true";

      userAnswers[currentQuestion] =
        option;
    };

    optionsContainer.appendChild(button);

  });


  document.getElementById("nextButton").textContent =
    currentQuestion === questions.length - 1
      ? "Finish Quiz"
      : "Next";
}


/* Next question */
function nextQuestion() {

  if (!userAnswers[currentQuestion]) {

    alert("Please select an answer.");

    return;
  }

  if (currentQuestion <
      questions.length - 1) {

    currentQuestion++;

    showQuestion();

  } else {

    showResults();
  }
}


/* Show results */
function showResults() {

  document
    .getElementById("quizScreen")
    .classList.add("hidden");

  document
    .getElementById("resultScreen")
    .classList.remove("hidden");

  let score = 0;

  questions.forEach((question, index) => {

    if (
      userAnswers[index] ===
      question.answer
    ) {

      score++;
    }

  });


  document.getElementById("resultName").textContent =
    `Name: ${playerName}`;

  document.getElementById("score").textContent =
    `${score} / ${questions.length}`;


  let message;

  if (score === 20) {

    message = "Perfect! You're a Doraemon expert!";

  } else if (score >= 15) {

    message = "Amazing! You really know Doraemon!";

  } else if (score >= 10) {

    message = "Nice! You know quite a lot about Doraemon.";

  } else {

    message = "Good try! Time for a Doraemon rewatch 😄";

  }

  document.getElementById("resultMessage").textContent =
    message;


  const review =
    document.getElementById("review");

  review.innerHTML = "";


  questions.forEach((question, index) => {

    const div =
      document.createElement("div");

    const isCorrect =
      userAnswers[index] === question.answer;

    div.className =
      "review-item " +
      (isCorrect ? "correct" : "wrong");


    div.innerHTML = `
      <strong>${index + 1}. ${question.question}</strong>
      <br><br>
      Your answer: ${userAnswers[index]}
      <br>
      Correct answer: ${question.answer}
    `;

    review.appendChild(div);

  });


  /*
    Save the completed result locally.
    This lets the browser remember the latest result.
  */

  const resultData = {

    name: playerName,

    score: score,

    answers: userAnswers,

    completedAt: new Date().toISOString()

  };


  localStorage.setItem(
    "doraemonQuizResult",
    JSON.stringify(resultData)
  );

}


/* Restart */
function restartQuiz() {

  document
    .getElementById("resultScreen")
    .classList.add("hidden");

  document
    .getElementById("startScreen")
    .classList.remove("hidden");

  document.getElementById("playerName").value = "";

}

</script>

</body>
</html>
