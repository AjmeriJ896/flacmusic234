<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Music Play Portal</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 20px;
            background-color: #ffb6c1; /* Light pink */
        }
        .container {
            max-width: 800px;
            margin: 0 auto;
            background-color: #f2e6ff; /* Very light purple */
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0,0,0,0.1);
        }
        .auth-section, .music-section, .future-section {
            margin-bottom: 30px;
        }
        input, button, textarea {
            padding: 10px;
            margin: 5px;
            border-radius: 5px;
            border: 1px solid #ddd;
        }
        .signin-btn {
            background-color: #4CAF50;
            color: white;
            cursor: pointer;
        }
        .signin-btn:hover {
            background-color: #45a049;
        }
        .login-btn {
            background-color: #ff0000;
            color: white;
            cursor: pointer;
        }
        .login-btn:hover {
            background-color: #cc0000;
        }
        .hidden {
            display: none;
        }
        .music-list {
            margin: 10px 0;
        }
        .music-list audio {
            width: 100%;
            margin: 10px 0;
        }
        .tab-buttons button {
            width: 48%;
            margin: 0 1%;
        }
        .music-section button {
            background-color: #4CAF50;
            color: white;
            cursor: pointer;
        }
        .music-section button:hover {
            background-color: #45a049;
        }
        textarea {
            width: 100%;
            height: 100px;
            resize: vertical;
        }
        .main-heading {
            text-align: center;
            color: #333;
            margin-bottom: 20px;
        }
        .future-section a {
            text-decoration: none;
            color: #0066cc;
            display: block;
            margin: 10px 0;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1 class="main-heading">ALL SONGS IN FLAC FORMAT AVAILABLE HERE</h1>

        <div class="auth-section" id="authSection">
            <div class="tab-buttons">
                <button class="signin-btn" onclick="showSignIn()">Sign In</button>
                <button class="login-btn" onclick="showLogIn()">Log In (Sign Up)</button>
            </div>

            <!-- Sign In Form -->
            <div id="signinForm">
                <h2>Sign In</h2>
                <input type="text" id="signinUsername" placeholder="Username" required>
                <input type="password" id="signinPassword" placeholder="Password" required>
                <button class="signin-btn" onclick="signIn()">Sign In</button>
                <p id="signinMessage"></p>
            </div>

            <!-- Log In (Sign Up) Form -->
            <div id="loginForm" class="hidden">
                <h2>Log In (Sign Up)</h2>
                <input type="text" id="loginUsername" placeholder="New Username" required>
                <input type="password" id="loginPassword" placeholder="New Password" required>
                <input type="password" id="confirmPassword" placeholder="Confirm Password" required>
                <button class="login-btn" onclick="logIn()">Sign Up</button>
                <p id="loginMessage"></p>
            </div>
        </div>

        <div class="music-section hidden" id="musicSection">
            <h2>Play Music</h2>
            <div class="music-list">
                <div>
                    <p>Sample Song - Test Track</p>
                    <audio controls>
                        <source src="https://www.kozco.com/tech/piano2.flac" type="audio/flac">
                        Your browser does not support the audio element.
                    </audio>
                </div>
            </div>
            
            <h3>Feedback</h3>
            <textarea id="feedbackText" placeholder="Yahan apna song likhkar bhejein..."></textarea>
            <button onclick="submitFeedback()">Submit Feedback</button>
            <p id="feedbackMessage"></p>

            <button onclick="signOut()">Sign Out</button>
        </div>

        <div class="future-section">
            <h2>Our Paid Plans</h2>
            <ul>
                <li>5 songs in 5$</li>
                <li>50 songs in 20$</li>
            </ul>
            <a href="https://pay.google.com/gp/w/u/0/home/sendmoney?amount=5¤cy=USD" target="_blank">Pay via GPay</a>
            <p>UPI ID: ajmerijuned7@oksbi</p>
            <br><br><br><br>
            <p>Payment karne ke baad apke choice likhkar humko bhejein. 24 hours ke andar paise wapas aa jayenge, trust issue ka koi khatra nahi hai. Agar aapko aisa lagta hai ki fraud hai, to pehle 1$ dekar 1 song purchase karke dekh lein.</p>
        </div>
    </div>

    <script>
        let users = {
            "user123": "pass123"
        };

        function showSignIn() {
            document.getElementById("signinForm").classList.remove("hidden");
            document.getElementById("loginForm").classList.add("hidden");
        }

        function showLogIn() {
            document.getElementById("loginForm").classList.remove("hidden");
            document.getElementById("signinForm").classList.add("hidden");
        }

        function signIn() {
            const username = document.getElementById("signinUsername").value;
            const password = document.getElementById("signinPassword").value;
            const message = document.getElementById("signinMessage");

            if (users[username] && users[username] === password) {
                document.getElementById("authSection").classList.add("hidden");
                document.getElementById("musicSection").classList.remove("hidden");
                message.textContent = "";
            } else {
                message.textContent = "Galat username ya password! Try again.";
                message.style.color = "red";
            }
        }

        function logIn() {
            const username = document.getElementById("loginUsername").value;
            const password = document.getElementById("loginPassword").value;
            const confirmPassword = document.getElementById("confirmPassword").value;
            const message = document.getElementById("loginMessage");

            if (!username || !password || !confirmPassword) {
                message.textContent = "Saare fields bharo!";
                message.style.color = "red";
                return;
            }

            if (password !== confirmPassword) {
                message.textContent = "Passwords match nahi karte!";
                message.style.color = "red";
                return;
            }

            if (users[username]) {
                message.textContent = "Ye username pehle se hai!";
                message.style.color = "red";
                return;
            }

            users[username] = password;
            message.textContent = "Sign Up successful! Ab Sign In karo.";
            message.style.color = "green";
            
            document.getElementById("loginUsername").value = "";
            document.getElementById("loginPassword").value = "";
            document.getElementById("confirmPassword").value = "";
        }

        function signOut() {
            document.getElementById("musicSection").classList.add("hidden");
            document.getElementById("authSection").classList.remove("hidden");
            document.getElementById("signinUsername").value = "";
            document.getElementById("signinPassword").value = "";
            document.getElementById("signinMessage").textContent = "";
            document.getElementById("feedbackText").value = "";
            document.getElementById("feedbackMessage").textContent = "";
        }

        function submitFeedback() {
            const feedback = document.getElementById("feedbackText").value;
            const message = document.getElementById("feedbackMessage");

            if (!feedback) {
                message.textContent = "Feedback khali nahi ho sakta!";
                message.style.color = "red";
                return;
            }

            message.textContent = "Feedback submit ho gaya! Shukriya!";
            message.style.color = "green";
            document.getElementById("feedbackText").value = "";
            setTimeout(() => {
                message.textContent = "";
            }, 3000);
        }

        showSignIn();
    </script>
</body>
</html>
