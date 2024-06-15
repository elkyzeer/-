<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Fifteen Puzzle</title>
    <style>
        /* General styles */
        body {
            font-family: 'Montserrat', sans-serif;
            text-align: center;
            background: linear-gradient(45deg, #ff9a9e, #fad0c4);
            color: #333;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }

        /* Tile styles */
        .tile {
            width: 60px;
            height: 60px;
            background-color: #fff;
            border-radius: 8px;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
            display: inline-block;
            text-align: center;
            line-height: 60px;
            margin: 4px;
            cursor: pointer;
            font-weight: bold;
            transition: all 0.2s ease;
        }

            .tile:hover {
                background-color: #f2f2f2;
                transform: scale(1.05);
            }

        .empty {
            visibility: hidden;
        }

        /* Container styles */
        .container {
            margin-top: 40px;
        }

        #startScreen {
            text-align: center;
        }

        /* Button styles */
        button {
            font-family: 'Montserrat', sans-serif;
            background-color: #ff6b6b;
            color: #fff;
            border: none;
            padding: 12px 24px;
            border-radius: 20px;
            cursor: pointer;
            transition: all 0.2s ease;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
        }

            button:hover {
                background-color: #ff4d4d;
                transform: scale(1.05);
            }

        /* Win message styles */
        #winMessage {
            font-size: 28px;
            color: #4caf50;
            margin-top: 30px;
            text-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
        }

        /* Main modal background styles */
        .modal {
            display: none;
            position: fixed;
            z-index: 1;
            left: 0;
            top: 0;
            width: 100%;
            height: 100%;
            overflow: auto;
            background-color: rgba(0, 0, 0, 0.4);
        }

        .modal-content {
            background-color: #fefefe;
            margin: 15% auto;
            padding: 20px;
            border: 1px solid #888;
            width: 30%;
            border-radius: 8px;
        }

        .close {
            color: #aaa;
            float: right;
            font-size: 28px;
            font-weight: bold;
        }

            .close:hover,
            .close:focus {
                color: black;
                text-decoration: none;
                cursor: pointer;
            }
    </style>
</head>
<body>
    <!-- Main screen with "Start" button -->
    <div id="startScreen">
        <button id="startButton" onclick="startGame()">Start Game</button>

        <!-- Prototype of the "Catalog" screen form -->
        <div id="catalogScreen">
            <h2>Catalog</h2>
            <div class="category-list">
                <button onclick="showCategory('antivirus')">Антівірус</button>
                <button onclick="showCategory('os')">Оперативна система</button>
                <button onclick="showCategory('office')">Офісні програми</button>
                <button onclick="showCategory('utilities')">Утиліта</button>
                <button onclick="showCategory('paymentmethod')">Спосіб оплати</button>
                <button onclick="showCategory('deliverymethod')">Спосіб доставки</button>
            </div>
            <div id="categoryContent"></div>
        </div>

        <!-- Prototype of the "Catalog/Payment Method" screen form -->
        <div id="soCategory" style="display: none;">
            <h3>Спосіб оплати</h3>
            <ul>
                <li>Тут буде вибір способу оплати</li>
            </ul>
        </div>

        <!-- Prototype of the "Catalog/Delivery Method" screen form -->
        <div id="sdCategory" style="display: none;">
            <h3>Спосіб доставки</h3>
            <ul>
                <li>Тут буде вибір способу доставки</li>
            </ul>
        </div>

        <!-- Prototype of the "Catalog/Antiviruses" screen form -->
        <div id="antivirusCategory" style="display: none;">
            <h3>Antiviruses</h3>
            <ul>
                <li>Antivirus A</li>
                <li>Antivirus B</li>
                <li>Antivirus C</li>
            </ul>
        </div>

        <!-- Prototype of the "Catalog/Operating Systems" screen form -->
        <div id="osCategory" style="display: none;">
            <h3>Operating Systems</h3>
            <ul>
                <li>OS X</li>
                <li>OS Y</li>
                <li>OS Z</li>
            </ul>
        </div>

        <!-- Prototype of the "Catalog/Office Programs" screen form -->
        <div id="officeCategory" style="display: none;">
            <h3>Office Programs</h3>
            <ul>
                <li>Office Suite A</li>
                <li>Office Suite B</li>
                <li>Office Suite C</li>
            </ul>
        </div>

        <!-- Prototype of the "Catalog/Utilities" screen form -->
        <div id="utilitiesCategory" style="display: none;">
            <h3>Utilities</h3>
            <ul>
                <li>Utility A</li>
                <li>Utility B</li>
                <li>Utility C</li>
            </ul>
        </div>

        <!-- Prototype of the "Delivery Method" screen form -->
        <div id="deliveryScreen" style="display: none;">
            <h2>Delivery Method</h2>
            <ul>
                <li>
                    <input type="radio" id="delivery1" name="delivery" value="option1">
                    <label for="delivery1">Delivery Option 1</label>
                </li>
                <li>
                    <input type="radio" id="delivery2" name="delivery" value="option2">
                    <label for="delivery2">Delivery Option 2</label>
                </li>
                <li>
                    <input type="radio" id="delivery3" name="delivery" value="option3">
                    <label for="delivery3">Delivery Option 3</label>
                </li>
            </ul>
        </div>

        <!-- Prototype of the "Payment Method" screen form -->
        <div id="paymentScreen" style="display: none;">
            <h2>Payment Method</h2>
            <ul>
                <li>
                    <input type="radio" id="payment1" name="payment" value="option1">
                    <label for="payment1">Payment Option 1</label>
                </li>
                <li>
                    <input type="radio" id="payment2" name="payment" value="option2">
                <li>
                    <input type="radio" id="payment2" name="payment" value="option2">
                    <label for="payment2">Payment Option 2</label>
                </li>
                <li>
                    <input type="radio" id="payment3" name="payment" value="option3">
                    <label for="payment3">Payment Option 3</label>
                </li>
            </ul>
        </div>
    </div>

    <!-- Game screen -->
    <div id="gameScreen" style="display: none;">
        <h1 id="gameTitle">Fifteen Puzzle</h1>
        <div id="board"></div>
        <div id="winMessage"></div>
        <div class="container">
            <button id="shuffleButton" onclick="shuffleBoard()">Shuffle</button>
            <button id="stopButton" onclick="openModal()">Stop</button>
        </div>
    </div>

    <!-- Modal -->
    <div id="modal" class="modal">
        <div class="modal-content">
            <span class="close" onclick="closeModal()">&times;</span>
            <p id="modalMessage">Do you want to save your progress and exit the game?</p>
            <button id="continueButton" onclick="continueGame()">Continue Game</button>
            <button id="exitButton" onclick="exitGame()">Exit Game</button>
        </div>
    </div>

    <script>
        // Variables for the game board
        var size = 4;
        var board = [];
        var emptyRow, emptyCol;
        var gameScreen = document.getElementById('gameScreen');
        var startScreen = document.getElementById('startScreen');
        var winMessage = document.getElementById('winMessage');
        var modal = document.getElementById('modal');

        // Saving the current game state
        var savedBoard = [];

        // Initialize the board and tiles
        function initBoard() {
            board = [];
            var k = 1;
            for (var i = 0; i < size; ++i) {
                var row = [];
                for (var j = 0; j < size; ++j) {
                    row.push(k++);
                }
                board.push(row);
            }
            emptyRow = size - 1;
            emptyCol = size - 1;
            board[emptyRow][emptyCol] = 0;
            shuffleBoard();
            renderBoard();
        }

        // Render the board
        function renderBoard() {
            var boardDiv = document.getElementById('board');
            boardDiv.innerHTML = '';
            for (var i = 0; i < size; ++i) {
                for (var j = 0; j < size; ++j) {
                    var tile = board[i][j];
                    var tileDiv = document.createElement('div');
                    tileDiv.classList.add('tile');
                    if (tile === 0) {
                        tileDiv.classList.add('empty');
                    } else {
                        tileDiv.textContent = tile;
                    }
                    tileDiv.setAttribute('data-row', i);
                    tileDiv.setAttribute('data-col', j);
                    tileDiv.onclick = function () {
                        moveTile(parseInt(this.getAttribute('data-row')), parseInt(this.getAttribute('data-col')));
                    };
                    boardDiv.appendChild(tileDiv);
                }
                boardDiv.appendChild(document.createElement('br'));
            }
        }

        // Move a tile
        function moveTile(row, col) {
            if ((row === emptyRow && Math.abs(col - emptyCol) === 1) ||
                (col === emptyCol && Math.abs(row - emptyRow) === 1)) {
                swapTiles(row, col, emptyRow, emptyCol);
            }
        }

        // Swap two tiles
        function swapTiles(row1, col1, row2, col2) {
            var temp = board[row1][col1];
            board[row1][col1] = board[row2][col2];
            board[row2][col2] = temp;
            emptyRow = row1;
            emptyCol = col1;
            renderBoard();
            if (checkGameOver()) {
                winMessage.textContent = "Congratulations! You won!";
            } else {
                winMessage.textContent = "";
            }
        }

        // Check if the game is over
        function checkGameOver() {
            var k = 1;
            for (var i = 0; i < size; ++i) {
                for (var j = 0; j < size; ++j) {
                    if (board[i][j] !== k && !(board[i][j] === 0 && k === size * size)) {
                        return false;
                    }
                    k++;
                }
            }
            return true;
        }

        // Shuffle the board
        function shuffleBoard() {
            for (var i = 0; i < 1000; ++i) {
                var randomRow = Math.floor(Math.random() * size);
                var randomCol = Math.floor(Math.random() * size);
                moveTile(randomRow, randomCol);
            }
        }

        // Start the game
        function startGame() {
            startScreen.style.display = 'none';
            gameScreen.style.display = 'block';
            winMessage.textContent = "";
            initBoard();
        }

        // Open the modal
        function openModal() {
            savedBoard = board.map(row => row.slice()); // Save a deep copy of the board
            modal.style.display = "block";
        }

        // Close the modal
        function closeModal() {
            modal.style.display = "none";
        }

        // Continue the game after closing the modal
        function continueGame() {
            closeModal();
            board = savedBoard.map(row => row.slice()); // Restore the saved board
            renderBoard();
        }

        // Exit the game after the modal
        function exitGame() {
            closeModal();
            gameScreen.style.display = 'none';
            startScreen.style.display = 'block';
            initBoard(); // Reset to the initial board state
        }

        // Event handler for pressing the Esc key
        window.addEventListener('keydown', function (event) {
            if (event.key === 'Escape' || event.key === 'Esc') {
                closeModal();
            }
        });

        // Function to display a category
        function showCategory(category) {
            var categoryContent = document.getElementById('categoryContent');
            var antivirusCategory = document.getElementById('antivirusCategory');
            var osCategory = document.getElementById('osCategory');
            var officeCategory = document.getElementById('officeCategory');
            var utilitiesCategory = document.getElementById('utilitiesCategory');
            var sdCategory = document.getElementById('sdCategory');
            var soCategory = document.getElementById('soCategory');

            // Hide all categories initially
            antivirusCategory.style.display = 'none';
            osCategory.style.display = 'none';
            officeCategory.style.display = 'none';
            utilitiesCategory.style.display = 'none';
            sdCategory.style.display = 'none';
            soCategory.style.display = 'none';

            // Show the selected category
            switch (category) {
                case 'antivirus':
                    categoryContent.innerHTML = '';
                    categoryContent.appendChild(antivirusCategory);
                    antivirusCategory.style.display = 'block';
                    break;
                case 'os':
                    categoryContent.innerHTML = '';
                    categoryContent.appendChild(osCategory);
                    osCategory.style.display = 'block';
                    break;
                case 'office':
                    categoryContent.innerHTML = '';
                    categoryContent.appendChild(officeCategory);
                    officeCategory.style.display = 'block';
                    break;
                case 'utilities':
                    categoryContent.innerHTML = '';
                    categoryContent.appendChild(utilitiesCategory);
                    utilitiesCategory.style.display = 'block';
                    break;
                case 'paymentmethod':
                    categoryContent.innerHTML = '';
                    categoryContent.appendChild(soCategory);
                    soCategory.style.display = 'block';
                    break;
                case 'deliverymethod':
                    categoryContent.innerHTML = '';
                    categoryContent.appendChild(sdCategory);
                    sdCategory.style.display = 'block';
                    break;
            }
            return true
        }

    </script>
</body>
</html>
