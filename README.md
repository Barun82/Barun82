<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Responsive Tic Tac Toe</title>
    <style>
      /* Basic reset */
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    font-family: 'Arial', sans-serif;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    background: linear-gradient(135deg, #ff9a9e, #fad0c4);
}

.container {
    text-align: center;
}

h1 {
    font-size: 2.5rem;
    color: #ffffff;
    text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5);
}

#game-board {
    display: grid;
    grid-template-columns: repeat(3, 100px);
    grid-template-rows: repeat(3, 100px);
    gap: 10px;
    justify-content: center;
    margin: 20px 0;
}

.cell {
    background-color: #ffffff;
    border-radius: 10px;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 2.5rem;
    font-weight: bold;
    color: #333;
    cursor: pointer;
    box

  </style>
</head>
<body>
    <div class="container">
        <h1>Tic Tac Toe</h1>
        <div id="game-board">
            <div class="cell" data-cell></div>
            <div class="cell" data-cell></div>
            <div class="cell" data-cell></div>
            <div class="cell" data-cell></div>
            <div class="cell" data-cell></div>
            <div class="cell" data-cell></div>
            <div class="cell" data-cell></div>
            <div class="cell" data-cell></div>
            <div class="cell" data-cell></div>
        </div>
        <h2 id="statusMessage"></h2>
        <button id="restartButton">Restart Game</button>
    </div>
    <script>const cells = document.querySelectorAll('[data-cell]');
const statusMessage = document.getElementById('statusMessage');
const restartButton = document.getElementById('restartButton');
let currentPlayer = 'X';
let board = Array(9).fill(null);
let gameActive = true;

const winningCombinations = [
    [0, 1, 2],
    [3, 4, 5],
    [6, 7, 8],
    [0, 3, 6],
    [1, 4, 7],
    [2, 5, 8],
    [0, 4, 8],
    [2, 4, 6]
];

// Handle cell clicks
cells.forEach(cell => {
    cell.addEventListener('click', handleCellClick, { once: true });
});

function handleCellClick(e) {
    const cell = e.target;
    const cellIndex = Array.from(cells).indexOf(cell);

    if (gameActive && !board[cellIndex]) {
        board[cellIndex] = currentPlayer;
        cell.innerText = currentPlayer;
        if (checkWin(currentPlayer)) {
            gameActive = false;
            statusMessage.innerText = `${currentPlayer} Wins!`;
        } else if (board.every(cell => cell)) {
            gameActive = false;
            statusMessage.innerText = 'Draw!';
        } else {
            currentPlayer = currentPlayer === 'X' ? 'O' : 'X';
            statusMessage.innerText = `Player ${currentPlayer}'s turn`;
        }
    }
}

// Check for a winner
function checkWin(player) {
    return winningCombinations.some(combination => {
        return combination.every(index => board[index] === player);
    });
}

// Restart the game
restartButton.addEventListener('click', restartGame);

function restartGame() {
    board.fill(null);
    cells.forEach(cell => {
        cell.innerText = '';
        cell.removeEventListener('click', handleCellClick);
        cell.addEventListener('click', handleCellClick, { once: true });
    });
    currentPlayer = 'X';
    gameActive = true;
    statusMessage.innerText = `Player ${currentPlayer}'s turn`;
}
</script>
</body>
</html>
