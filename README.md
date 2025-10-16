# tic-to-tac-game
game 
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Tic-Tac-Toe</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      text-align: center;
      margin-top: 50px;
    }

    h1 {
      margin-bottom: 20px;
    }

    #board {
      display: grid;
      grid-template-columns: repeat(3, 100px);
      grid-template-rows: repeat(3, 100px);
      gap: 5px;
      justify-content: center;
      margin: 0 auto;
    }

    .cell {
      width: 100px;
      height: 100px;
      font-size: 2.5em;
      background-color: #f0f0f0;
      border: 2px solid #333;
      display: flex;
      align-items: center;
      justify-content: center;
      cursor: pointer;
      user-select: none;
    }

    .cell:hover {
      background-color: #e0e0e0;
    }

    #msg {
      margin-top: 20px;
      font-size: 1.4em;
    }

    #reset {
      margin-top: 15px;
      padding: 10px 20px;
      font-size: 1em;
      cursor: pointer;
    }
  </style>
</head>
<body>

  <h1>Tic-Tac-Toe</h1>
  <div id="board"></div>
  <p id="msg">Player X's turn</p>
  <button id="reset">Restart Game</button>

  <script>
    const board = document.getElementById('board');
    const msg = document.getElementById('msg');
    const resetBtn = document.getElementById('reset');

    let cells = Array(9).fill('');
    let currentPlayer = 'X';
    let gameActive = true;

    function createBoard() {
      board.innerHTML = '';
      cells = Array(9).fill('');
      currentPlayer = 'X';
      gameActive = true;
      msg.textContent = "Player X's turn";

      for (let i = 0; i < 9; i++) {
        const cell = document.createElement('div');
        cell.className = 'cell';
        cell.dataset.index = i;
        cell.addEventListener('click', handleMove);
        board.appendChild(cell);
      }
    }

    function handleMove(e) {
      const index = e.target.dataset.index;

      if (!gameActive || cells[index] !== '') return;

      cells[index] = currentPlayer;
      e.target.textContent = currentPlayer;

      if (checkWinner()) {
        msg.textContent = `Player ${currentPlayer} wins!`;
        gameActive = false;
        return;
      }

      if (!cells.includes('')) {
        msg.textContent = "It's a draw!";
        gameActive = false;
        return;
      }

      currentPlayer = currentPlayer === 'X' ? 'O' : 'X';
      msg.textContent = `Player ${currentPlayer}'s turn`;
    }

    function checkWinner() {
      const winPatterns = [
        [0,1,2], [3,4,5], [6,7,8],
        [0,3,6], [1,4,7], [2,5,8],
        [0,4,8], [2,4,6]
      ];

      return winPatterns.some(pattern => {
        const [a, b, c] = pattern;
        return cells[a] && cells[a] === cells[b] && cells[a] === cells[c];
      });
    }

    resetBtn.addEventListener('click', createBoard);
    createBoard();
  </script>
</body>
</html>

