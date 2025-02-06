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
        .hidden {
            display: none;
        }
        .question {
            background-color: #ecf0f1;
            padding: 10px;
            margin: 5px 0;
            border-radius: 5px;
        }
        .delete-btn {
            background-color: red;
            color: white;
            border: none;
            padding: 5px;
            cursor: pointer;
            border-radius: 5px;
        }
        .admin-panel {
            margin-top: 20px;
        }
    </style>
</head>
<body>

    <h1>مرحبًا بك في موقع الأسئلة والأجوبة!</h1>
    
    <div class="container">
        <h3>إضافة سؤال جديد:</h3>
        <input type="text" id="new-question" placeholder="اكتب سؤالك هنا..." />
        <button onclick="addQuestion()">إضافة السؤال</button>
    </div>

    <div class="container">
        <h3>الأسئلة غير المجابة:</h3>
        <div id="questions-list"></div>
    </div>

    <div class="container">
        <h3>الأسئلة المجابة:</h3>
        <div id="answered-questions"></div>
    </div>

    <div class="container">
        <button onclick="toggleAdminPanel()">تسجيل الدخول كإدمن</button>
    </div>

    <div id="admin-login" class="container hidden">
        <h3>تسجيل الدخول للإدمن:</h3>
        <input type="text" id="username" placeholder="اسم المستخدم" /><br><br>
        <input type="password" id="password" placeholder="كلمة المرور" /><br><br>
        <button onclick="login()">تسجيل الدخول</button>
        <div id="login-error" style="color: red; display: none;">اسم المستخدم أو كلمة المرور غير صحيحة!</div>
    </div>

    <div id="admin-panel" class="container hidden">
        <h3>لوحة تحكم الإدمن</h3>
        <button onclick="logout()">تسجيل الخروج</button>
        <button onclick="deleteAllQuestions()">مسح جميع الأسئلة</button>
    </div>

    <script>
        const adminUsername = "admin";
        const adminPassword = "password123";
        let isAdminLoggedIn = false;

        function loadQuestions() {
            const questions = JSON.parse(localStorage.getItem("questions")) || [];
            let unansweredHTML = '';
            let answeredHTML = '';

            questions.forEach((q, index) => {
                if (!q.answer) {
                    unansweredHTML += `
                        <div class="question">
                            <p>${q.question}</p>
                            ${isAdminLoggedIn ? `<button onclick="startAnswering(${index})">الإجابة</button>
                            <button class="delete-btn" onclick="deleteQuestion(${index})">حذف</button>` : ''}
                        </div>
                    `;
                } else {
                    answeredHTML += `
                        <div class="question">
                            <p><strong>السؤال:</strong> ${q.question}</p>
                            <p><strong>الإجابة:</strong> ${q.answer}</p>
                        </div>
                    `;
                }
            });

            document.getElementById('questions-list').innerHTML = unansweredHTML;
            document.getElementById('answered-questions').innerHTML = answeredHTML;
        }

        function addQuestion() {
            const questionText = document.getElementById("new-question").value.trim();
            if (questionText === "") {
                alert("يرجى إدخال سؤال");
                return;
            }

            const questions = JSON.parse(localStorage.getItem("questions")) || [];
            questions.push({ question: questionText, answer: "" });
            localStorage.setItem("questions", JSON.stringify(questions));

            document.getElementById("new-question").value = "";
            loadQuestions();
        }

        function toggleAdminPanel() {
            document.getElementById("admin-login").classList.toggle("hidden");
        }

        function login() {
            var username = document.getElementById('username').value;
            var password = document.getElementById('password').value;

            if (username === adminUsername && password === adminPassword) {
                isAdminLoggedIn = true;
                document.getElementById("admin-login").classList.add("hidden");
                document.getElementById("admin-panel").classList.remove("hidden");
                loadQuestions();
            } else {
                document.getElementById('login-error').style.display = 'block';
            }
        }

        function logout() {
            isAdminLoggedIn = false;
            document.getElementById("admin-panel").classList.add("hidden");
            loadQuestions();
        }

        function startAnswering(index) {
            const answer = prompt("اكتب إجابتك هنا:");
            if (answer) {
                const questions = JSON.parse(localStorage.getItem("questions")) || [];
                questions[index].answer = answer;
                localStorage.setItem("questions", JSON.stringify(questions));
                loadQuestions();
            }
        }

        function deleteAllQuestions() {
            if (confirm("هل أنت متأكد من مسح جميع الأسئلة؟")) {
                localStorage.removeItem("questions");
                loadQuestions();
            }
        }

        function deleteQuestion(index) {
            const questions = JSON.parse(localStorage.getItem("questions")) || [];
            questions.splice(index, 1);
            localStorage.setItem("questions", JSON.stringify(questions));
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

        loadQuestions();
    </script>
</body>
</html>
