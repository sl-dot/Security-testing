      
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tetris</title>
    <style>
        #tetris {
            width: 200px;
            height: 400px;
            background-color: black;
            display: grid;
            grid-template-columns: repeat(10, 1fr);
            grid-gap: 1px;
        }
      .cell {
            background-color: white;
            border: 1px solid black;
        }
      .filled {
            background-color: red;
        }
    </style>
</head>
<body>
    <div id="tetris"></div>
    <script>
        const tetris = document.getElementById('tetris');
        const cells = [];
        const rows = 20;
        const cols = 10;

        for (let i = 0; i < rows * cols; i++) {
            const cell = document.createElement('div');
            cell.classList.add('cell');
            tetris.appendChild(cell);
            cells.push(cell);
        }

        function drawGrid(grid) {
            for (let i = 0; i < rows; i++) {
                for (let j = 0; j < cols; j++) {
                    const index = i * cols + j;
                    if (grid[i][j] === 1) {
                        cells[index].classList.add('filled');
                    } else {
                        cells[index].classList.remove('filled');
                    }
                }
            }
        }

        let grid = Array.from({ length: rows }, () => Array(cols).fill(0));

        function createPiece() {
            const pieces = [
                [[1, 1], [1, 1]],
                [[1, 1, 1, 1]],
                [[1, 1, 0], [0, 1, 1]],
                [[0, 1, 1], [1, 1, 0]],
                [[1, 1, 1], [0, 1, 0]],
                [[1, 1, 1], [1, 0, 0]],
                [[1, 1, 1], [0, 0, 1]]
            ];
            const piece = pieces[Math.floor(Math.random() * pieces.length)];
            return piece;
        }

        let currentPiece = createPiece();
        let pieceRow = 0;
        let pieceCol = 3;

        function drawPiece() {
            for (let i = 0; i < currentPiece.length; i++) {
                for (let j = 0; j < currentPiece[0].length; j++) {
                    if (currentPiece[i][j] === 1) {
                        const index = (pieceRow + i) * cols + (pieceCol + j);
                        cells[index].classList.add('filled');
                    }
                }
            }
        }

        function clearPiece() {
            for (let i = 0; i < currentPiece.length; i++) {
                for (let j = 0; j < currentPiece[0].length; j++) {
                    if (currentPiece[i][j] === 1) {
                        const index = (pieceRow + i) * cols + (pieceCol + j);
                        cells[index].classList.remove('filled');
                    }
                }
            }
        }

        function movePieceDown() {
            if (!checkCollision(pieceRow + 1, pieceCol)) {
                clearPiece();
                pieceRow++;
                drawPiece();
            } else {
                mergePiece();
                currentPiece = createPiece();
                pieceRow = 0;
                pieceCol = 3;
                drawPiece();
            }
        }

        function checkCollision(newRow, newCol) {
            for (let i = 0; i < currentPiece.length; i++) {
                for (let j = 0; j < currentPiece[0].length; j++) {
                    if (currentPiece[i][j] === 1) {
                        const row = newRow + i;
                        const col = newCol + j;
                        if (row >= rows || col < 0 || col >= cols || grid[row][col] === 1) {
                            return true;
                        }
                    }
                }
            }
            return false;
        }

        function mergePiece() {
            for (let i = 0; i < currentPiece.length; i++) {
                for (let j = 0; j < currentPiece[0].length; j++) {
                    if (currentPiece[i][j] === 1) {
                        const index = (pieceRow + i) * cols + (pieceCol + j);
                        grid[Math.floor(index / cols)][index % cols] = 1;
                    }
                }
            }
        }

        function rotatePiece() {
            const rotated = [];
            for (let j = 0; j < currentPiece[0].length; j++) {
                const newRow = [];
                for (let i = currentPiece.length - 1; i >= 0; i--) {
                    newRow.push(currentPiece[i][j]);
                }
                rotated.push(newRow);
            }
            if (!checkCollision(pieceRow, pieceCol, rotated)) {
                clearPiece();
                currentPiece = rotated;
                drawPiece();
            }
        }

        document.addEventListener('keydown', (event) => {
            if (event.key === 'ArrowLeft') {
                if (!checkCollision(pieceRow, pieceCol - 1)) {
                    clearPiece();
                    pieceCol--;
                    drawPiece();
                }
            } else if (event.key === 'ArrowRight') {
                if (!checkCollision(pieceRow, pieceCol + 1)) {
                    clearPiece();
                    pieceCol++;
                    drawPiece();
                }
            } else if (event.key === 'ArrowDown') {
                movePieceDown();
            } else if (event.key === 'ArrowUp') {
                rotatePiece();
            }
        });

        setInterval(movePieceDown, 1000);
    </script>
</body>
</html>

    
