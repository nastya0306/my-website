let playerName = '';
let playerScore = 0;
let computerScore = 0;
let roundCount = 0;
let maxRounds = 3;

document.getElementById('start-game').addEventListener('click', startGame);
document.getElementById('next-round').addEventListener('click', nextRound);
document.getElementById('restart-game').addEventListener('click', restartGame);

function startGame() {
    playerName = document.getElementById('name').value.trim();
    if (!playerName) {
        alert('Будь ласка, введіть своє ім\'я!');
        return;
    }

    document.getElementById('player-name').classList.add('hidden');
    document.getElementById('game').classList.remove('hidden');
    playRound();
}

function playRound() {
    if (roundCount >= maxRounds) {
        declareWinner();
        return;
    }

    roundCount++;

    const playerNumber = Math.floor(Math.random() * 100) + 1;
    const computerNumber = Math.floor(Math.random() * 100) + 1;

    document.getElementById('player-number').textContent = playerNumber;
    document.getElementById('computer-number').textContent = computerNumber;

    let roundResult = '';
    if (playerNumber > computerNumber) {
        playerScore++;
        roundResult = `${playerName} виграв раунд!`;
    } else if (playerNumber < computerNumber) {
        computerScore++;
        roundResult = `Комп'ютер виграв раунд!`;
    } else {
        roundResult = 'Нічия!';
    }

    document.getElementById('round-result').textContent = roundResult;
    document.getElementById('score').textContent = `${playerScore} - ${computerScore}`;
}

function nextRound() {
    playRound();
}

function declareWinner() {
    let winnerMessage = '';
    if (playerScore > computerScore) {
        winnerMessage = `${playerName} виграв гру!`;
    } else if (playerScore < computerScore) {
        winnerMessage = 'Комп\'ютер виграв гру!';
    } else {
        winnerMessage = 'Гра закінчилась внічию!';
    }

    document.getElementById('game').classList.add('hidden');
    document.getElementById('winner').classList.remove('hidden');
    document.getElementById('winner-message').textContent = winnerMessage;
}

function restartGame() {
    playerScore = 0;
    computerScore = 0;
    roundCount = 0;
    document.getElementById('score').textContent = `${playerScore} - ${computerScore}`;
    document.getElementById('round-result').textContent = '';
    document.getElementById('player-name').classList.remove('hidden');
    document.getElementById('winner').classList.add('hidden');
    document.getElementById('name').value = '';
}  
