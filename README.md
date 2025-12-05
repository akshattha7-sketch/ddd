# ddd
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Hello Divisha</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #ffe6f2; /* Light pink background */
            color: #d63384; /* Darker pink text */
            text-align: center;
            padding: 20px;
            overflow: hidden; /* Prevent scrollbars from confetti */
        }
        .container {
            max-width: 600px;
            margin: 0 auto;
            background-color: #ffb3d9; /* Medium pink */
            border-radius: 10px;
            padding: 20px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            position: relative;
            z-index: 1;
        }
        .hearts {
            font-size: 24px;
            margin: 10px 0;
        }
        .slide {
            opacity: 0;
            transform: translateX(100%);
            transition: opacity 0.5s ease-in-out, transform 0.5s ease-in-out;
        }
        .slide.active {
            opacity: 1;
            transform: translateX(0);
        }
        .conversation {
            margin-bottom: 20px;
        }
        .message {
            margin-bottom: 10px;
            padding: 10px;
            background-color: #ff99cc; /* Lighter pink */
            border-radius: 5px;
        }
        button {
            background-color: #ff66b2; /* Bright pink */
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 5px;
            cursor: pointer;
            font-size: 16px;
            margin: 5px;
            transition: background-color 0.3s;
        }
        button:hover {
            background-color: #ff4da6;
        }
        .game {
            margin-top: 20px;
        }
        .board {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 5px;
            width: 150px;
            margin: 0 auto;
            transition: transform 0.3s;
        }
        .cell {
            width: 50px;
            height: 50px;
            background-color: #ff99cc;
            border: 1px solid #d63384;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 24px;
            cursor: pointer;
            transition: background-color 0.3s, transform 0.2s;
        }
        .cell:hover {
            background-color: #ffb3d9;
            transform: scale(1.05);
        }
        .status {
            margin-top: 10px;
            font-weight: bold;
            transition: color 0.5s, transform 0.5s;
        }
        .status.animate {
            animation: pulse 1s infinite;
        }
        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.1); }
            100% { transform: scale(1); }
        }
        .board.animate {
            animation: shake 0.5s;
        }
        @keyframes shake {
            0%, 100% { transform: translateX(0); }
            25% { transform: translateX(-5px); }
            75% { transform: translateX(5px); }
        }
        /* Confetti styles */
        .confetti {
            position: absolute;
            width: 10px;
            height: 10px;
            background-color: #ff66b2;
            animation: fall 3s linear infinite;
            z-index: 0;
        }
        .confetti:nth-child(odd) {
            background-color: #ffb3d9;
        }
        .confetti:nth-child(3n) {
            background-color: #ff99cc;
        }
        @keyframes fall {
            0% { transform: translateY(-100vh) rotate(0deg); }
            100% { transform: translateY(100vh) rotate(360deg); }
        }
        .celebration {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            font-size: 48px;
            animation: bounce 1s infinite;
            z-index: 2;
        }
        @keyframes bounce {
            0%, 20%, 50%, 80%, 100% { transform: translate(-50%, -50%) translateY(0); }
            40% { transform: translate(-50%, -50%) translateY(-10px); }
            60% { transform: translate(-50%, -50%) translateY(-5px); }
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Hello Divisha 💕</h1>
        <div class="hearts">❤️ 💖 💕 💗 💓</div>
        
        <!-- Slide 1: Initial message -->
        <div class="slide active" id="slide1">
            <div class="conversation">
                <div class="message">Hello Divisha</div>
            </div>
            <button onclick="replyHiAkshat()">Hi Akshat</button>
        </div>
        
        <!-- Slide 2: Will you play a game? -->
        <div class="slide" id="slide2">
            <div class="conversation">
                <div class="message">Hello Divisha</div>
                <div class="message">Hi Akshat</div>
            </div>
            <div class="message">Will you play a game?</div>
            <button onclick="yesToGame()">Yes</button>
        </div>
        
        <!-- Slide 3: Tic Tac Toe Game -->
        <div class="slide" id="slide3">
            <div class="conversation">
                <div class="message">Hello Divisha</div>
                <div class="message">Hi Akshat</div>
                <div class="message">Will you play a game?</div>
                <div class="message">Yes</div>
            </div>
            <div class="game">
                <h2>Play Tic Tac Toe!</h2>
                <div class="board" id="board">
                    <div class="cell" data-index="0"></div>
                    <div class="cell" data-index="1"></div>
                    <div class="cell" data-index="2"></div>
                    <div class="cell" data-index="3"></div>
                    <div class="cell" data-index="4"></div>
                    <div class="cell" data-index="5"></div>
                    <div class="cell" data-index="6"></div>
                    <div class="cell" data-index="7"></div>
                    <div class="cell" data-index="8"></div>
                </div>
                <div class="status" id="status">Your turn! (You are X)</div>
                <button onclick="resetGame()">Reset Game</button>
            </div>
        </div>
    </div>

    <script>
        function replyHiAkshat() {
            const current = document.querySelector('.slide.active');
            const next = document.getElementById('slide2');
            current.classList.remove('active');
            next.classList.add('active');
        }

        function yesToGame() {
            const current = document.querySelector('.slide.active');
            const next = document.getElementById('slide3');
            current.classList.remove('active');
            next.classList.add('active');
        }

        // Tic Tac Toe logic
        const boardElement = document.getElementById('board');
        const cells = document.querySelectorAll('.cell');
        const status = document.getElementById('status');
        let gameBoard = ['', '', '', '', '', '', '', '', ''];
        let currentPlayer = 'X'; // Human is X, AI is O
        let gameActive = true;

        cells.forEach(cell => {
            cell.addEventListener('click', handleCellClick);
        });

        function handleCellClick(event) {
            const index = event.target.dataset.index;
            if (gameBoard[index] !== '' || !gameActive) return;

            gameBoard[index] = currentPlayer;
            event.target.textContent = currentPlayer;
            checkWinner();

            if (gameActive) {
                currentPlayer = 'O';
                status.textContent = "AI's turn...";
                setTimeout(aiMove, 500); // Delay for AI move
            }
        }

        function aiMove() {
            let bestMove = getBestMove();
            gameBoard[bestMove] = 'O';
            cells[bestMove].textContent = 'O';
            checkWinner();
            if (gameActive) {
                currentPlayer = 'X';
                status.textContent = "Your turn! (You are X)";
            }
        }

        function getBestMove() {
            let bestScore = -Infinity;
            let move;
            for (let i = 0; i < 9; i++) {
                if (gameBoard[i] === '') {
                    gameBoard[i] = 'O';
                    let score = minimax(gameBoard, 0, false);
                    gameBoard[i] = '';
                    if (score > bestScore) {
                        bestScore = score;
                        move = i;
                    }
                }
            }
            return move;
        }

        function minimax(board, depth, isMaximizing) {
            let result = checkWinnerMinimax();
            if (result !== null) {
                return result;
            }

            if (isMaximizing) {
                let bestScore = -Infinity;
                for (let i = 0; i < 9; i++) {
                    if (board[i] === '') {
                        board[i] = 'O';
                        let score = minimax(board, depth + 1, false);
                        board[i] = '';
                        bestScore = Math.max(score, bestScore);
                    }
                }
                return bestScore;
            } else {
                let bestScore = Infinity;
                for (let i = 0; i < 9; i++) {
                    if (board[i] === '') {
                        board[i] = 'X';
                        let score = minimax(board, depth + 1, true);
                        board[i] = '';
                        bestScore = Math.min(score, bestScore);
                    }
                }
                return bestScore;
            }
        }

        function checkWinnerMinimax() {
            const winConditions = [
                [0, 1, 2], [3, 4, 5], [6, 7, 8],
                [0, 3, 6], [1, 4, 7], [2, 5, 8],
                [0, 4, 8], [2, 4, 6]
            ];

            for (let condition of winConditions) {
                const [a, b, c] = condition;
                if (gameBoard[a] && gameBoard[a] === gameBoard[b] && gameBoard[a] === gameBoard[c]) {
                    if (gameBoard[a] === 'O') return 10; // AI wins
                    if (gameBoard[a] === 'X') return -10; // Human wins
                }
            }

            if (gameBoard.every(cell => cell !== '')) return 0; // Tie
            return null; // Game continues
        }

        function checkWinner() {
            const winConditions = [
                [0, 1, 2], [3, 4, 5], [6, 7, 8],
                [0, 3, 6], [1, 4, 7], [2, 5, 8],
                [0, 4, 8], [2, 4, 6]
            ];

            for (let condition of winConditions) {
                const [a, b, c] = condition;
                if (gameBoard[a] && gameBoard[a] === gameBoard[b] && gameBoard[a] === gameBoard[c]) {
                    if (gameBoard[a] === 'X') {
                        status.textContent = "You win! 🎉";
                        status.classList.add('animate');
                        boardElement.classList.add('animate');
                        startCelebration();
                    } else {
                        status.textContent = "AI wins!";
                        status.classList.add('animate');
                        boardElement.classList.add('animate');
                    }
                    gameActive = false;
                    return;
                }
            }

            if (gameBoard.every(cell => cell !== '')) {
                status.textContent = "It's a tie! 🎉";
                status.classList.add('animate');
                boardElement.classList.add('animate');
                startCelebration();
                gameActive = false;
                return;
            }
        }

        function startCelebration() {
            // Create confetti
            for (let i = 0; i < 50; i++) {
                const confetti = document.createElement('div');
                confetti.className = 'confetti';
                confetti.style.left = Math.random() * 100 + 'vw';
                confetti.style.animationDelay = Math.random() * 3 + 's';
                document.body.appendChild(confetti);
                setTimeout(() => confetti.remove(), 3000);
            }
            // Add bouncing celebration emoji
            const celebration = document.createElement('div');
            celebration.className = 'celebration';
            celebration.textContent = '🎉';
            document.body.appendChild(celebration);
            setTimeout(() => celebration.remove(), 3000);
        }

        function resetGame() {
            gameBoard = ['', '', '', '', '', '', '', '', ''];
            cells.forEach(cell => cell.textContent = '');
            currentPlayer = 'X';
            gameActive = true;
            status.textContent = "Your turn! (You are X)";
            status.classList.remove('animate');
            boardElement.classList.remove('animate');
        }
    </script>
</body>
</html>
