function playSound(id) {
    let sound = document.getElementById(id);
    sound.currentTime = 0; // Sound ko restart karne ke liye
    sound.play();
}

function playTurn() {
    if (wickets[0] >= maxWickets && wickets[1] >= maxWickets) {
        checkWinner();
        return;
    }

    // Dice roll sound
    playSound("sound-dice");

    let dice = Math.floor(Math.random() * 6) + 1;
    let diceIcon = ["", "⚀", "⚁", "⚂", "⚃", "⚄", "⚅"];
    document.getElementById("dice-display").innerHTML = diceIcon[dice];

    let status = document.getElementById("status-msg");

    if (dice === 5) {
        if (isFreeHit[currentPlayer]) {
            status.innerHTML = `🛡️ SAFE! Free Hit bach gaya!`;
            isFreeHit[currentPlayer] = false;
        } else {
            wickets[currentPlayer]++;
            status.innerHTML = `☝️ OUT! Player ${currentPlayer + 1} gaya!`;
            playSound("sound-out"); // Out sound
            changeTurn();
        }
    } 
    else if (dice === 6) {
        scores[currentPlayer] += 6;
        status.innerHTML = `🚀 SIXER!!! Extra Turn!`;
        playSound("sound-hit"); // Hit sound
    }
    else if (dice === 4) {
        scores[currentPlayer] += 4;
        isFreeHit[currentPlayer] = true;
        status.innerHTML = `🏏 CHAUUKA! Free Hit mila!`;
        playSound("sound-hit"); // Hit sound
        changeTurn();
    }
    else {
        scores[currentPlayer] += dice;
        status.innerHTML = `Player ${currentPlayer + 1}: ${dice} runs`;
        isFreeHit[currentPlayer] = false;
        changeTurn();
    }

    updateUI();
}
function playSound(id) {
    let sound = document.getElementById(id);
    sound.currentTime = 0; // Sound ko restart karne ke liye
    sound.play();
}

function playTurn() {
    if (wickets[0] >= maxWickets && wickets[1] >= maxWickets) {
        checkWinner();
        return;
    }

    // Dice roll sound
    playSound("sound-dice");

    let dice = Math.floor(Math.random() * 6) + 1;
    let diceIcon = ["", "⚀", "⚁", "⚂", "⚃", "⚄", "⚅"];
    document.getElementById("dice-display").innerHTML = diceIcon[dice];

    let status = document.getElementById("status-msg");

    if (dice === 5) {
        if (isFreeHit[currentPlayer]) {
            status.innerHTML = `🛡️ SAFE! Free Hit bach gaya!`;
            isFreeHit[currentPlayer] = false;
        } else {
            wickets[currentPlayer]++;
            status.innerHTML = `☝️ OUT! Player ${currentPlayer + 1} gaya!`;
            playSound("sound-out"); // Out sound
            changeTurn();
        }
    } 
    else if (dice === 6) {
        scores[currentPlayer] += 6;
        status.innerHTML = `🚀 SIXER!!! Extra Turn!`;
        playSound("sound-hit"); // Hit sound
    }
    else if (dice === 4) {
        scores[currentPlayer] += 4;
        isFreeHit[currentPlayer] = true;
        status.innerHTML = `🏏 CHAUUKA! Free Hit mila!`;
        playSound("sound-hit"); // Hit sound
        changeTurn();
    }
    else {
        scores[currentPlayer] += dice;
        status.innerHTML = `Player ${currentPlayer + 1}: ${dice} runs`;
        isFreeHit[currentPlayer] = false;
        changeTurn();
    }

    updateUI();
}
# My-ludo-cricket-game
