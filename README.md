<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>1~100 숫자 맞추기 게임</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            padding: 30px;
        }

        h1 {
            color: #4CAF50;
        }

        .game-container {
            margin-top: 20px;
            font-size: 1.2em;
        }

        #message {
            font-size: 1.3em;
            margin: 20px;
            color: #FF5733;
        }

        input {
            font-size: 1.2em;
            padding: 10px;
            margin: 10px;
            width: 50%;
            max-width: 200px;
            text-align: center;
        }

        button {
            font-size: 1.2em;
            padding: 10px 20px;
            background-color: #4CAF50;
            color: white;
            border: none;
            cursor: pointer;
        }

        button:hover {
            background-color: #45a049;
        }

        .hidden {
            display: none;
        }
    </style>
</head>
<body>

    <h1>1~100 숫자 맞추기 게임</h1>
    <p>게임의 목표는 1부터 100 사이의 랜덤한 숫자를 맞추는 것입니다. 기회는 총 5번 주어집니다.</p>
    <p>각 기회마다 힌트를 통해 숫자가 더 크거나 작은지 알려드립니다.</p>

    <div class="game-container">
        <p id="message">숫자를 맞추세요!</p>
        <input type="number" id="userGuess" min="1" max="100" placeholder="1부터 100까지 숫자 입력" />
        <button onclick="checkGuess()">숫자 맞추기</button>
    </div>

    <div id="restartButton" class="hidden">
        <button onclick="restartGame()">다시 시작</button>
    </div>

    <script>
        let numberToGuess = Math.floor(Math.random() * 100) + 1;  // 랜덤 숫자 (1~100)
        let attempts = 5;  // 기회

        // 숫자 맞추기 함수
        function checkGuess() {
            const userGuess = parseInt(document.getElementById('userGuess').value);
            const message = document.getElementById('message');

            if (isNaN(userGuess) || userGuess < 1 || userGuess > 100) {
                message.textContent = "1과 100 사이의 숫자를 입력하세요!";
                return;
            }

            if (userGuess < numberToGuess) {
                attempts--;
                message.textContent = `더 큰 숫자입니다. 남은 기회: ${attempts}`;
            } else if (userGuess > numberToGuess) {
                attempts--;
                message.textContent = `더 작은 숫자입니다. 남은 기회: ${attempts}`;
            } else {
                message.textContent = `축하합니다! ${numberToGuess}을(를) 맞추셨습니다.`;
                document.getElementById('restartButton').classList.remove('hidden');
                return;
            }

            if (attempts <= 0) {
                message.textContent = `기회를 다 사용하셨습니다. 정답은 ${numberToGuess}였습니다.`;
                document.getElementById('restartButton').classList.remove('hidden');
            }
        }

        // 게임 재시작 함수
        function restartGame() {
            numberToGuess = Math.floor(Math.random() * 100) + 1;
            attempts = 5;
            document.getElementById('userGuess').value = '';
            document.getElementById('message').textContent = "숫자를 맞추세요!";
            document.getElementById('restartButton').classList.add('hidden');
        }
    </script>

</body>
</html>
