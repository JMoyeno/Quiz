# Quiz
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Quiz App</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            background-image: url(Quiz1.png);
      background-size: cover;
      background-position: center;
      background-repeat: no-repeat;
      background-attachment: fixed;
        }

        h1 {
            color: #333;
        }

        .quiz-container {
            max-width: 500px;
            margin: 0 auto;
        }

        .question {
            margin-bottom: 20px;
        }

        .options {
            display: flex;
            flex-direction: column;
            align-items: flex-start;
        }

        .option {
            margin: 10px 0;
        }

        #score {
            margin-top: 20px;
        }
    </style>
</head>
<body>
    <h1>Quiz App</h1>
    <div class="quiz-container">
        <div class="question" id="question"></div>
        <div class="options" id="options"></div>
        <button id="next-button">Next</button>
        <div id="score"></div>
        <button id="reload-button" style="display: none">Reload and Start Again</button>
    </div>

    <script>
        const questions = [
            {
                question: "What is the capital of France?",
                options: ["London", "Berlin", "Paris", "Madrid"],
                answer: "Paris"
            },
            {
                question: "Which planet is known as the Red Planet?",
                options: ["Earth", "Mars", "Venus", "Jupiter"],
                answer: "Mars"
            },
            {
                question: "What is the largest mammal in the world?",
                options: ["Elephant", "Blue Whale", "Giraffe", "Hippopotamus"],
                answer: "Blue Whale"
            }
        ];

        const questionElement = document.getElementById("question");
        const optionsElement = document.getElementById("options");
        const nextButton = document.getElementById("next-button");
        const scoreElement = document.getElementById("score");
        const reloadButton = document.getElementById("reload-button");

        let currentQuestion = 0;
        let score = 0;

        function loadQuestion() {
            if (currentQuestion < questions.length) {
                questionElement.textContent = questions[currentQuestion].question;
                optionsElement.innerHTML = "";
                questions[currentQuestion].options.forEach((option) => {
                    const label = document.createElement("label");
                    label.classList.add("option");
                    const radio = document.createElement("input");
                    radio.type = "radio";
                    radio.name = "option";
                    radio.value = option;
                    label.appendChild(radio);
                    label.appendChild(document.createTextNode(option));
                    optionsElement.appendChild(label);
                });
                nextButton.disabled = true;
            } else {
                showScore();
            }
        }

        function showScore() {
            questionElement.textContent = "Quiz Complete";
            optionsElement.innerHTML = "";
            scoreElement.textContent = `Your Score: ${score} out of ${questions.length}`;
            nextButton.style.display = "none";
            reloadButton.style.display = "block";
        }

        loadQuestion();

        nextButton.addEventListener("click", function () {
            const selectedOption = document.querySelector('input[name="option"]:checked');
            if (selectedOption) {
                if (selectedOption.value === questions[currentQuestion].answer) {
                    score++;
                }
                currentQuestion++;
                loadQuestion();
            }
        });

        reloadButton.addEventListener("click", function () {
            currentQuestion = 0;
            score = 0;
            loadQuestion();
            scoreElement.textContent = "";
            reloadButton.style.display = "none";
            nextButton.style.display = "block";
        });
    </script>
</body>
</html>
