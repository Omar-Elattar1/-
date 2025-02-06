<!DOCTYPE html>
<html lang="ar">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>موقع الأسئلة والأجوبة</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f9;
            text-align: center;
            direction: rtl;
            margin: 0;
            padding: 0;
        }
        h1 {
            color: #2c3e50;
        }
        .container {
            width: 90%;
            max-width: 800px;
            margin: 20px auto;
            padding: 20px;
            background-color: #fff;
            border-radius: 10px;
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
        }
        #login-section, #admin-panel, #answer-page {
            display: none;
        }
        #login-error {
            color: red;
            display: none;
        }
        .question {
            background-color: #ecf0f1;
            padding: 10px;
            margin: 5px 0;
            border-radius: 5px;
        }
    </style>
</head>
<body>

<h1>مرحبًا بك في صفحة الأسئلة والأجوبة!</h1>

<div id="login-section" class="container">
    <h3>تسجيل الدخول للإجابة على الأسئلة:</h3>
    <input type="text" id="username" placeholder="اسم المستخدم"><br><br>
    <input type="password" id="password" placeholder="كلمة المرور"><br><br>
    <button onclick="login()">تسجيل الدخول</button>
    <div id="login-error">اسم المستخدم أو كلمة المرور غير صحيحة!</div>
</div>

<div id="admin-panel" class="container">
    <h3>الأسئلة غير المجابة:</h3>
    <div id="questions-list"></div>
    <button onclick="deleteAllQuestions()">مسح جميع الأسئلة</button>
</div>

<div id="answer-page" class="container">
    <h3>إجابة السؤال</h3>
    <p id="current-question"></p>
    <textarea id="answer" placeholder="اكتب إجابتك هنا..." rows="4" cols="50"></textarea><br><br>
    <button onclick="submitAnswer()">إرسال الإجابة</button>
</div>

<script>
    const adminUsername = "admin";
    const adminPassword = "password123";
    let isAdminLoggedIn = false;
    let currentQuestionIndex = 0;

    function loadQuestions() {
        const questions = JSON.parse(localStorage.getItem("questions")) || [];
        let questionListHTML = '';

        questions.forEach((q, index) => {
            if (!q.answer) {
                questionListHTML += `
                    <div class="question">
                        <p>${q.question}</p>
                        <button onclick="startAnswering(${index})">الإجابة</button>
                    </div>
                `;
            }
        });

        document.getElementById('questions-list').innerHTML = questionListHTML;
    }

    function login() {
        var username = document.getElementById('username').value;
        var password = document.getElementById('password').value;

        if (username === adminUsername && password === adminPassword) {
            isAdminLoggedIn = true;
            document.getElementById('login-section').style.display = 'none';
            document.getElementById('admin-panel').style.display = 'block';
            loadQuestions();
        } else {
            document.getElementById('login-error').style.display = 'block';
        }
    }

    function startAnswering(index) {
        if (!isAdminLoggedIn) {
            alert("يجب عليك تسجيل الدخول أولاً كإدمن");
            return;
        }

        var questions = JSON.parse(localStorage.getItem("questions")) || [];
        currentQuestionIndex = index;
        document.getElementById('current-question').innerText = "السؤال: " + questions[currentQuestionIndex].question;
        document.getElementById('answer-page').style.display = "block";
    }

    function submitAnswer() {
        if (!isAdminLoggedIn) {
            alert("يجب عليك تسجيل الدخول أولاً كإدمن");
            return;
        }

        var answerText = document.getElementById('answer').value.trim();
        if (answerText !== "") {
            var questions = JSON.parse(localStorage.getItem("questions")) || [];
            questions[currentQuestionIndex].answer = answerText;
            localStorage.setItem("questions", JSON.stringify(questions));

            document.getElementById('answer').value = "";
            document.getElementById('answer-page').style.display = "none";
            loadQuestions();
        } else {
            alert("يرجى كتابة إجابة أولاً!");
        }
    }

    function deleteAllQuestions() {
        localStorage.removeItem("questions");
        loadQuestions();
    }

    function addSampleQuestions() {
        const sampleQuestions = [
            { question: "ما هو اسمك؟", answer: "" },
            { question: "ما هي هواياتك؟", answer: "" },
            { question: "ما هو لونك المفضل؟", answer: "" }
        ];
        localStorage.setItem("questions", JSON.stringify(sampleQuestions));
    }

    if (!localStorage.getItem("questions")) {
        addSampleQuestions();
    }

    document.addEventListener("DOMContentLoaded", function() {
        document.getElementById('login-section').style.display = 'block';
    });
</script>

</body>
</html>
