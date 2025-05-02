<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title>Tic Tac Toe</title>
    <style>
        body {
            font-family: 'Segoe UI', sans-serif;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 100vh;
            background: #f2f2f2;
        }
        
        h1 {
            margin-bottom: 20px;
        }
        
        #game-board {
            display: grid;
            grid-template-columns: repeat(3, 100px);
            grid-template-rows: repeat(3, 100px);
            gap: 5px;
        }
        
        .cell {
            background-color: #fff;
            border: 2px solid #444;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 2.5rem;
            cursor: pointer;
            user-select: none;
            transition: background 0.3s ease;
        }
        
        .cell:hover {
            background-color: #e0e0e0;
        }
        
        #message {
            margin-top: 20px;
            font-size: 1.2rem;
        }
        
        button {
            margin-top: 15px;
            padding: 10px 20px;
            font-size: 1rem;
            cursor: pointer;
            background-color: #007bff;
            color: white;
            border: none;
            border-radius: 5px;
        }
        
        button:hover {
            background-color: #0056b3;
        }
    </style>
</head>

<body>

    <h1>Tic Tac Toe</h1>
    <div id="game-board">
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

    <div id="message">Player X's turn</div>
    <button onclick="resetGame()">Restart Game</button>

    <script>
        let currentPlayer = 'X';
        let gameState = ['', '', '', '', '', '', '', '', ''];
        const winningCombos = [
            [0, 1, 2],
            [3, 4, 5],
            [6, 7, 8],
            [0, 3, 6],
            [1, 4, 7],
            [2, 5, 8],
            [0, 4, 8],
            [2, 4, 6]
        ];

        const cells = document.querySelectorAll('.cell');
        const message = document.getElementById('message');

        cells.forEach(cell => {
            cell.addEventListener('click', handleClick);
        });

        function handleClick(e) {
            const index = e.target.dataset.index;
            if (gameState[index] !== '' || checkWinner()) return;

            gameState[index] = currentPlayer;
            e.target.textContent = currentPlayer;

            if (checkWinner()) {
                message.textContent = `Player ${currentPlayer} wins!`;
            } else if (!gameState.includes('')) {
                message.textContent = "It's a draw!";
            } else {
                currentPlayer = currentPlayer === 'X' ? 'O' : 'X';
                message.textContent = `Player ${currentPlayer}'s turn`;
            }
        }

        function checkWinner() {
            return winningCombos.some(combo => {
                return combo.every(i => gameState[i] === currentPlayer);
            });
        }

        function resetGame() {
            gameState = ['', '', '', '', '', '', '', '', ''];
            currentPlayer = 'X';
            message.textContent = `Player ${currentPlayer}'s turn`;
            cells.forEach(cell => cell.textContent = '');
        }
    </script>

</body>

</html>
