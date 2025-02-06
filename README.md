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
        #login-section, #admin-panel {
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
        .answer-box {
            margin: 20px 0;
        }
        #answer-page {
            display: none;
        }
        .delete-btn {
            background-color: red;
            color: white;
            border: none;
            padding: 5px;
            cursor: pointer;
            border-radius: 5px;
        }
    </style>
</head>
<body>

    <h1>مرحبًا بك في صفحة الأسئلة والأجوبة!</h1>
    
    <div id="login-section" class="container">
        <h3>تسجيل الدخول للإجابة على الأسئلة:</h3>
        <input type="text" id="username" placeholder="اسم المستخدم" /><br><br>
        <input type="password" id="password" placeholder="كلمة المرور" /><br><br>
        <button onclick="login()">تسجيل الدخول</button>
        <div id="login-error">اسم المستخدم أو كلمة المرور غير صحي
