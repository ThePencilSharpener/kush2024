---
layout: post
type: hacks
title: Cookie Clicker
search_exclude: true
permalink: /cookieclicker/
---



<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cookie Clicker Game</title>
    <style>
        body {
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            height: 100vh;
            background-color: #f0e68c;
            font-family: Arial, sans-serif;
            text-align: center;
        }
        #cookie {
            width: 200px;
            height: 200px;
            background-color: #e2b000;
            border-radius: 50%;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.5);
            margin-bottom: 20px;
            cursor: pointer;
        }
        #score {
            font-size: 2em;
            margin-bottom: 20px;
        }
        #upgrade {
            padding: 10px 20px;
            font-size: 1.5em;
            background-color: #4CAF50;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            transition: background-color 0.3s;
        }
        #upgrade:hover {
            background-color: #45a049;
        }
    </style>
</head>
<body>
    <div id="score">Cookies: 0</div>
    <div id="cookie" onclick="addCookie()"></div>
    <button id="upgrade" onclick="upgrade()">Upgrade (Cost: 10 cookies)</button>
    <audio controls>
        <source src="nomnom.mp3">
    <script>
        let cookies = 0;
        let cookieMultiplier = 1;
        const scoreElement = document.getElementById('score');
        function addCookie() {
            cookies += cookieMultiplier;
            updateScore();
        }
        function updateScore() {
            scoreElement.innerText = `Cookies: ${cookies}`;
        }
        function upgrade() {
            if (cookies >= 10) {
                cookies -= 10;
                cookieMultiplier++;
                updateScore();
            } else {
                alert('Not enough cookies for an upgrade!');
            }
        }
    </script>
</body>

