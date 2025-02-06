<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>الموقع الرسمي للشيخ أحمد حمدي</title>
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
            margin-bottom: 20px;
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
        input, button {
            width: 100%;
            max-width: 300px;
            margin: 10px auto;
            padding: 10px;
            border: 1px solid #ccc;
            border-radius: 5px;
            font-size: 16px;
        }
        button {
            background-color: #3498db;
            color: white;
            cursor: pointer;
        }
        button:hover {
            background-color: #2980b9;
        }
        .section {
            margin: 20px 0;
        }
        .social-links {
            margin: 20px 0;
            display: flex;
            justify-content: center;
            gap: 10px;
        }
        .social-links a {
            padding: 10px 20px;
            border-radius: 5px;
            color: white;
            text-decoration: none;
            font-weight: bold;
        }
        .tiktok { background-color: #ff0050; }
        .instagram { background-color: #c13584; }
        .youtube { background-color: #ff0000; }
        .question-box {
            background-color: #f4f4f9;
            padding: 10px;
            border-radius: 5px;
            margin: 10px 0;
            text-align: right;
            position: relative;
        }
        .question-box button {
            width: auto;
            padding: 5px 10px;
            font-size: 14px;
            margin-left: 10px;
        }
        .footer {
            margin-top: 30px;
            font-size: 14px;
            color: gray;
        }
        .footer .green {
            color: green;
            font-size: 16px;
            font-weight: bold;
        }
        .footer a {
            color: gray;
            text-decoration: none;
        }
    </style>
</head>
<body>
    <h1>الموقع الرسمي للشيخ أحمد حمدي</h1>
    <div class="container">
        <div class="section">
            <h2>إضافة سؤال جديد:</h2>
            <input id="new-question" type="text" placeholder="اكتب سؤالك هنا...">
            <button onclick="addQuestion()">إضافة السؤال</button>
        </div>
        <div class="section">
            <h2>الأسئلة غير المجابة:</h2>
            <div id="unanswered-questions">
                <!-- قائمة الأسئلة غير المجابة -->
            </div>
        </div>
        <div class="section">
            <h2>الأسئلة المجابة:</h2>
            <div id="answered-questions">
                <!-- قائمة الأسئلة المجابة -->
            </div>
        </div>
        <div class="section">
            <h2>تابع الشيخ أحمد حمدي على:</h2>
            <div class="social-links">
                <a href="#" class="tiktok">تيك توك</a>
                <a href="#" class="instagram">إنستجرام</a>
                <a href="#" class="youtube">يوتيوب</a>
            </div>
        </div>
        <button style="margin: 20px auto; display: block; border: 1px solid black; background-color: white; color: black;">تسجيل الدخول كأدمن</button>
        <div class="footer">
            <p class="green">صل على النبي ﷺ</p>
            <p>تم الإنشاء بواسطة عمر</p>
        </div>
    </div>

    <script>
        function addQuestion() {
            const questionText = document.getElementById("new-question").value;
            if (questionText.trim() === "") {
                alert("الرجاء كتابة سؤال أولاً!");
                return;
            }

            const unansweredSection = document.getElementById("unanswered-questions");

            const questionBox = document.createElement("div");
            questionBox.classList.add("question-box");

            questionBox.innerHTML = `
                <p><strong>السؤال:</strong> ${questionText}</p>
                <button onclick="answerQuestion(this)">إجابة</button>
                <button onclick="deleteQuestion(this)">حذف</button>
            `;

            unansweredSection.appendChild(questionBox);
            document.getElementById("new-question").value = "";
        }

        function answerQuestion(button) {
            const questionBox = button.parentElement;
            const answeredSection = document.getElementById("answered-questions");

            const answer = prompt("أدخل الإجابة:");
            if (answer && answer.trim() !== "") {
                const answerBox = document.createElement("div");
                answerBox.classList.add("question-box");

                answerBox.innerHTML = `
                    <p><strong>السؤال:</strong> ${questionBox.querySelector("p").innerText.replace("السؤال: ", "")}</p>
                    <p><strong>الإجابة:</strong> ${answer}</p>
                `;

                answeredSection.appendChild(answerBox);
                questionBox.remove();
            } else {
                alert("لم يتم إدخال إجابة!");
            }
        }

        function deleteQuestion
