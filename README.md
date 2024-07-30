

<head>
    <title>Login Page</title>
    <link href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css" rel="stylesheet">
    <style>
        body {
            background-image: url('bg2.jpg');
            background-size: cover;
            background-position: center;
            background-repeat: no-repeat;
            background-attachment: fixed;
            margin: 0;
            padding: 0;
            font-family: Arial, sans-serif;
            background-color: #313131;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }
        .login-container {
            display: flex;
            flex-direction: row;
            width: 600px;
            background-color: rgba(249, 249, 249, 0.7);
            border-radius: 5px;
            box-shadow: 0 0 10px rgba(0,0,0,0.1);
            z-index: 1;
        }
        .login-form {
            flex: 1;
            padding: 20px;
        }
        .login-form h2 {
            color: #333;
            text-align: center;
            margin-bottom: 20px;
        }
        .login-form input[type="text"],
        .login-form input[type="password"] {
            width: 100%;
            padding: 8px;
            margin-bottom: 15px;
            border: 1px solid #ccc;
            border-radius: 3px;
            box-sizing: border-box;
        }
        .login-form input[type="submit"] {
            width: 100%;
            padding: 8px;
            border: none;
            background-color: #FF0000;
            color: #fff;
            border-radius: 3px;
            cursor: pointer;
        }
        .login-form input[type="submit"]:hover {
            background-color: #333;
        }
        .create-account {
            text-align: center;
            margin-top: 20px;
        }
        .create-account a {
            color: #FF0000;
            text-decoration: none;
        }
        .create-account a:hover {
            text-decoration: underline;
        }
        .recent-user {
            flex: 1;
            background-color: rgba(249, 249, 249, 0.5);
            border-left: 1px solid #ccc;
            padding: 20px;
            text-align: center;
        }
        .navbar {
            background: #FF0000; /* Neon Red background color of the navbar */
            box-shadow: 0 4px 8px rgba(255, 0, 0, 0.3); /* Neon Red box shadow for depth effect */
        }

        .navbar-brand {
            font-size: 24px;
            color: white;
            text-transform: uppercase;
        }

        .navbar-nav {
            display: flex;
            align-items: center;
        }

        .nav-item {
            margin: 0 10px;
        }

        .nav-link {
            font-size: 18px;
            color: #ff005d; /* Neon Red text color */
            position: relative;
            padding: 10px;
            transition: 0.3s;
        }

        .spinner-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(255, 255, 255, 0);
            display: flex;
            justify-content: center;
            align-items: center;
            z-index: 1000;
            display: none; /* Hidden by default */
        }

        /* Fullscreen Video Styles */
        #videoOverlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: black;
            display: flex;
            justify-content: center;
            align-items: center;
            z-index: 10;
        }

        #videoOverlay video {
            width: 100%;
            height: 100%;
            object-fit: cover;
        }

        #skipButton {
            position: absolute;
            top: 20px;
            right: 20px;
            background-color: rgba(0, 0, 0, 0.5);
            color: white;
            border: none;
            padding: 10px;
            cursor: pointer;
            z-index: 20;
        }
    </style>
</head>
<body>
    <nav class="navbar navbar-expand-lg navbar-dark bg-dark fixed-top">
        <a class="navbar-brand" href="#">Quirk App</a>
    </nav>

    <!-- Video Overlay -->
    <div id="videoOverlay">
        <video id="introVideo" autoplay muted>
            <source src="intro.mp4" type="video/mp4">
           
        </video>
        <button id="skipButton">Skip</button>
    </div>

    <div class="login-container">
        <div class="login-form">
            <h2>Login</h2>
            <form id="loginForm">
                <input type="text" name="username" id="username" placeholder="Username" required><br>
                <input type="password" name="password" id="password" placeholder="Password" required><br>
                <input type="submit" value="Login">
            </form>
            <div class="create-account">
                <span>Don't have an account? <a href="file:///C:/Users/Neil%20Porciuncula/OneDrive/Documents/html/Create_acc.html#">Create here</a></span>
            </div>
        </div>
        <div class="recent-user">
            <h2>Recent Login</h2>
            <p id="recentUsername">Username: None</p>
        </div>
    </div>

    <!-- Spinner Overlay -->
    <div class="spinner-overlay">
        <div class="spinner-border text-danger" role="status">
            <span class="visually-hidden"></span>
        </div>
    </div>

    <script>
        const users = {
            "Neil Porciuncula": "MY_Portfolio.html",
            "Jeanne Marielle Yarcia": "YARCIA.html",
            "Diosdado Tac-an": "TAC-AN.html",
            "Ronuald Joseph Reig": "REIG.html",
            "Jude Simon Gacul": "GACUL.html",
            "Mark Harry De Leon": "DE_LEON.html",
            "Reciel Marie Licuanan": "LICUANAN.html",
            "Manuel Alano": "ALANO.html"
        };

        document.getElementById('loginForm').addEventListener('submit', function(event) {
            event.preventDefault();
            var username = document.getElementById('username').value;
            var password = document.getElementById('password').value;

            if (users[username] && password === 'BSIT_302D') {
                localStorage.setItem('recentUser', username);
                document.querySelector('.spinner-overlay').style.display = 'flex'; // Show spinner
                setTimeout(function() {
                    window.location.href = users[username];
                }, 3000); // Delay to show the spinner 
            } else {
                alert('Incorrect username or password');
            }
        });

        document.addEventListener('DOMContentLoaded', function() {
            var recentUser = localStorage.getItem('recentUser');
            if (recentUser) {
                document.getElementById('recentUsername').textContent = "Username: " + recentUser;
            }

            var video = document.getElementById('introVideo');
            var videoOverlay = document.getElementById('videoOverlay');
            var skipButton = document.getElementById('skipButton');

            video.addEventListener('ended', function() {
                videoOverlay.style.display = 'none';
            });

            skipButton.addEventListener('click', function() {
                videoOverlay.style.display = 'none';
                video.pause();
            });
        });
    </script>
</body>
</html>
