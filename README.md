<!DOCTYPE html>
<html>
<head>
    <title>My Ludo Cricket Game</title>
    <style>
        /* Yahan wahi CSS design jo maine pehle diya tha */
        body { font-family: Arial; text-align: center; background: #f0f4f8; }
        .game-box { border: 5px solid #333; padding: 20px; width: 300px; margin: 20px auto; background: white; border-radius: 15px; }
        .active { background: #d1ffd1; border: 2px solid green; }
        button { padding: 10px 20px; font-size: 18px; cursor: pointer; }
    </style>
</head>
<body>

<div class="game-box">
    <h2>Ludo-Cricket 🏏</h2>
    <div id="status-msg">Game Shuru Karo!</div>
    <div id="p1-card" class="player-card active">P1 Runs: <span id="p1-runs">0</span> | W: <span id="p1-wickets">0</span></div>
    <div id="p2-card" class="player-card">P2 Runs: <span id="p2-runs">0</span> | W: <span id="p2-wickets">0</span></div>
    <div id="dice-display" style="font-size: 50px; margin: 10px;">🎲</div>
    <button onclick="playTurn()">Roll Dice</button>
</div>

<script>
    let scores = [0, 0]; 
    let wickets = [0, 0];
    let currentPlayer = 0;
    const maxWickets = 3;
    let isFreeHit = [false, false];

    function playTurn() {
        if (wickets[0] >= maxWickets && wickets[1] >= maxWickets) {
            alert("Game Over!");
            return;
        }
        let dice = Math.floor(Math.random() * 6) + 1;
        document.getElementById("dice-display").innerHTML = ["","⚀","⚁","⚂","⚃","⚄","⚅"][dice];
        
        // Baki ka pura logic yahan paste karein...
        if(dice === 5) { wickets[currentPlayer]++; }
        else { scores[currentPlayer] += dice; }
        
        updateUI();
        currentPlayer = (currentPlayer === 0) ? 1 : 0;
    }

    function updateUI() {
        document.getElementById("p1-runs").innerText = scores[0];
        document.getElementById("p1-wickets").innerText = wickets[0];
        document.getElementById("p2-runs").innerText = scores[1];
        document.getElementById("p2-wickets").innerText = wickets[1];
    }
</script>

</body>
</html>
<!DOCTYPE html>
<html>
<head>
    <title>My Ludo Cricket Game</title>
    <style>
        /* Yahan wahi CSS design jo maine pehle diya tha */
        body { font-family: Arial; text-align: center; background: #f0f4f8; }
        .game-box { border: 5px solid #333; padding: 20px; width: 300px; margin: 20px auto; background: white; border-radius: 15px; }
        .active { background: #d1ffd1; border: 2px solid green; }
        button { padding: 10px 20px; font-size: 18px; cursor: pointer; }
    </style>
</head>
<body>

<div class="game-box">
    <h2>Ludo-Cricket 🏏</h2>
    <div id="status-msg">Game Shuru Karo!</div>
    <div id="p1-card" class="player-card active">P1 Runs: <span id="p1-runs">0</span> | W: <span id="p1-wickets">0</span></div>
    <div id="p2-card" class="player-card">P2 Runs: <span id="p2-runs">0</span> | W: <span id="p2-wickets">0</span></div>
    <div id="dice-display" style="font-size: 50px; margin: 10px;">🎲</div>
    <button onclick="playTurn()">Roll Dice</button>
</div>

<script>
    let scores = [0, 0]; 
    let wickets = [0, 0];
    let currentPlayer = 0;
    const maxWickets = 3;
    let isFreeHit = [false, false];

    function playTurn() {
        if (wickets[0] >= maxWickets && wickets[1] >= maxWickets) {
            alert("Game Over!");
            return;
        }
        let dice = Math.floor(Math.random() * 6) + 1;
        document.getElementById("dice-display").innerHTML = ["","⚀","⚁","⚂","⚃","⚄","⚅"][dice];
        
        // Baki ka pura logic yahan paste karein...
        if(dice === 5) { wickets[currentPlayer]++; }
        else { scores[currentPlayer] += dice; }
        
        updateUI();
        currentPlayer = (currentPlayer === 0) ? 1 : 0;
    }

    function updateUI() {
        document.getElementById("p1-runs").innerText = scores[0];
        document.getElementById("p1-wickets").innerText = wickets[0];
        document.getElementById("p2-runs").innerText = scores[1];
        document.getElementById("p2-wickets").innerText = wickets[1];
    }
</script>

</body>
</html>

