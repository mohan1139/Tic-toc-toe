# Tic-toc-toe
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Tic-Tac-Toe</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      text-align: center;
      background: #f0f0f0;
      margin: 0;
      padding: 20px;
    }
    h1 {
      margin-bottom: 10px;
    }
    #gameBoard {
      display: grid;
      grid-template-columns: repeat(3, 100px);
      gap: 5px;
      justify-content: center;
      margin: 20px auto;
    }
    .cell {
      width: 100px;
      height: 100px;
      background: white;
      border: 2px solid #333;
      font-size: 2em;
      display: flex;
      align-items: center;
      justify-content: center;
      cursor: pointer;
    }
    .cell:hover {
      background: #e0e0e0;
    }
    #status {
      font-size: 1.2em;
      margin: 15px 0;
    }
    button {
      padding: 10px 20px;
      font-size: 1em;
      cursor: pointer;
    }
  </style>
</head>
<body>
  <h1>Tic-Tac-Toe</h1>
   
  <div id="status">Current Player: X</div>
  <div id="gameBoard"></div>
  <button onclick="resetGame()">Restart Game</button>

  <script>
    const board = document.getElementById("gameBoard");
    const status = document.getElementById("status");
    let currentPlayer = "X";
    let cells = Array(9).fill(null);
    let gameActive = true;

    function createBoard() {
      board.innerHTML = "";
      cells = Array(9).fill(null);
      gameActive = true;
      status.textContent = `Current Player: ${currentPlayer}`;
      for (let i = 0; i < 9; i++) {
        const cell = document.createElement("div");
        cell.classList.add("cell");
        cell.dataset.index = i;
        cell.addEventListener("click", makeMove);
        board.appendChild(cell);
      }
    }

    function makeMove(e) {
      const index = e.target.dataset.index;
      if (!cells[index] && gameActive) {
        cells[index] = currentPlayer;
        e.target.textContent = currentPlayer;
        if (checkWinner()) {
          status.textContent = `Player ${currentPlayer} wins!`;
          gameActive = false;
        } else if (!cells.includes(null)) {
          status.textContent = "It's a draw!";
          gameActive = false;
        } else {
          currentPlayer = currentPlayer === "X" ? "O" : "X";
          status.textContent = `Current Player: ${currentPlayer}`;
        }
      }
    }

    function checkWinner() {
      const winPatterns = [
        [0, 1, 2], [3, 4, 5], [6, 7, 8], // rows
        [0, 3, 6], [1, 4, 7], [2, 5, 8], // columns
        [0, 4, 8], [2, 4, 6]             // diagonals
      ];
      return winPatterns.some(pattern =>
        pattern.every(index => cells[index] === currentPlayer)
      );
    }

    function resetGame() {
      currentPlayer = "X";
      createBoard();
    }

    createBoard();
  </script>
</body>
</html>
