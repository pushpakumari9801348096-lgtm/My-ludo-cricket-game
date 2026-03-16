<!DOCTYPE html>
<html lang="hi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ludo Cricket Fusion</title>
    <style>
        body { font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; text-align: center; background-color: #e3f2fd; margin: 0; padding: 20px; }
        .game-box { background: white; max-width: 400px; margin: auto; padding: 20px; border-radius: 20px; box-shadow: 0 10px 30px rgba(0,0,0,0.2); border: 4px solid #1565c0; }
        h1 { color: #1565c0; font-size: 24px; margin-bottom: 10px; }
        .status-bar { background: #ffeb3b; padding: 10px; border-radius: 10px; font-weight: bold; margin-bottom: 20px; min-height: 25px; }
        .players-container { display: flex; justify-content: space-around; margin-bottom: 20px; }
        .player-card { padding: 15px; border-radius: 15px; border: 2px solid #ccc; width: 40%; transition: 0.3s; }
        .active { border-color: #2e7d32; background-color: #c8e6c9; transform: scale(1.1); box-shadow: 0 5px 15px rgba(0,0,0,0.1); }
        .dice-area { font-size: 80px; margin: 20px 0; cursor: pointer; user-select: none; }
        button { background-color: #1565c0; color: white; border: none; padding: 15px 30px; font-size: 18px; border-radius: 50px; cursor: pointer; transition: 0.2s; box-shadow: 0 4px #0d47a1; }
        button:active { box-shadow: 0 0 #0d47a1; transform: translateY(4px); }
        .score-val { font-size: 20px; font-weight: bold; display: block; }
    </style>
</head>
<body>

<div class="game-box">
    <h1>Ludo-Cricket Fusion 🏏</h1>
    <div id="status-msg" class="status-bar">Game Shuru Karein!</div>

    <div class="players-container">
        <div id="p1-card" class="player-card active">
            <strong>Player 1</strong><br>
            <span class="score-val">Runs: <span id="p1-runs">0</span></span>
            <span>Wkts: <span id="p1-wickets">0</span>/3</span>
        </div>
        <div id="p2-card" class="player-card">
            <strong>Player 2</strong><br>
            <span class="score-val">Runs: <span id="p2-runs">0</span></span>
            <span>Wkts: <span id="p2-wickets">0</span>/3</span>
        </div>
    </div>

    <div class="dice-area" id="dice-display" onclick="playTurn()">🎲</div>
    <button onclick="playTurn()">DICE ROLL</button>
</div>

<audio id="sound-hit" src="https://www.soundjay.com/buttons/sounds/button-3.mp3"></audio>
<audio id="sound-out" src="https://www.soundjay.com/buttons/sounds/button-10.mp3"></audio>
<audio id="sound-dice" src="https://www.soundjay.com/buttons/sounds/button-20.mp3"></audio>

<script>
    let scores = [0, 0]; 
    let wickets = [0, 0];
    let currentPlayer = 0; 
    let isFreeHit = [false, false];
    const maxWickets = 3;

    function playSound(id) {
        let sound = document.getElementById(id);
        sound.currentTime = 0;
        sound.play().catch(e => console.log("Sound play blocked"));
    }

    function playTurn() {
        if (wickets[0] >= maxWickets && wickets[1] >= maxWickets) {
            checkWinner();
            return;
        }

        playSound("sound-dice");
        let dice = Math.floor(Math.random() * 6) + 1;
        const diceIcons = ["", "⚀", "⚁", "⚂", "⚃", "⚄", "⚅"];
        document.getElementById("dice-display").innerHTML = diceIcons[dice];

        let status = document.getElementById("status-msg");

        if (dice === 5) {
            if (isFreeHit[currentPlayer]) {
                status.innerHTML = `🛡️ Player ${currentPlayer + 1} SAFE! Free Hit tha!`;
                isFreeHit[currentPlayer] = false;
            } else {
                wickets[currentPlayer]++;
                status.innerHTML = `☝️ OUT! Player ${currentPlayer + 1} gaya!`;
                playSound("sound-out");
                if (wickets[currentPlayer] < maxWickets) changeTurn();
            }
        } 
        else if (dice === 6) {
            scores[currentPlayer] += 6;
            status.innerHTML = `🚀 SIXER!!! Extra Turn mila!`;
            playSound("sound-hit");
        }
        else if (dice === 4) {
            scores[currentPlayer] += 4;
            isFreeHit[currentPlayer] = true;
            status.innerHTML = `🏏 CHAUUKA! Agla ball Free Hit!`;
            playSound("sound-hit");
            changeTurn();
        }
        else {
            scores[currentPlayer] += dice;
            status.innerHTML = `Player ${currentPlayer + 1} ne ${dice} runs liye.`;
            isFreeHit[currentPlayer] = false;
            changeTurn();
        }

        updateUI();
    }

    function changeTurn() {
        if (wickets[0] < maxWickets && wickets[1] < maxWickets) {
            currentPlayer = (currentPlayer === 0) ? 1 : 0;
            document.getElementById("p1-card").classList.toggle("active");
            document.getElementById("p2-card").classList.toggle("active");
        } else if (wickets[0] >= maxWickets && wickets[1] < maxWickets) {
            currentPlayer = 1;
            document.getElementById("p1-card").classList.remove("active");
            document.getElementById("p2-card").classList.add("active");
        } else if (wickets[1] >= maxWickets && wickets[0] < maxWickets) {
            currentPlayer = 0;
            document.getElementById("p2-card").classList.remove("active");
            document.getElementById("p1-card").classList.add("active");
        }
    }

    function updateUI() {
        document.getElementById("p1-runs").innerText = scores[0];
        document.getElementById("p1-wickets").innerText = wickets[0];
        document.getElementById("p2-runs").innerText = scores[1];
        document.getElementById("p2-wickets").innerText = wickets[1];

        if (wickets[0] >= maxWickets && wickets[1] >= maxWickets) {
            checkWinner();
        }
    }

    function checkWinner() {
        let msg = "";
        if (scores[0] > scores[1]) msg = "🏆 PLAYER 1 JEET GAYA!";
        else if (scores[1] > scores[0]) msg = "🏆 PLAYER 2 JEET GAYA!";
        else msg = "MATCH DRAW! 🤝";
        document.getElementById("status-msg").innerHTML = msg;
    }
</script>
</body>
</html>

        

