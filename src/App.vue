<template>
  <div id="app">
    <h1 class="title">เป่ายิงฉุบความมืด</h1>

    <div class="players">
      <div class="player">
        <h2>Player1</h2>
        <p class="score">Score: {{ player1Score }}</p>
        <div class="choice">
          <img v-if="!player1Choice" src="./assets/default.png" />
          <img v-if="player1Choice === 'rock.png'" src='./assets/rock.png' alt="Rock" />
          <img v-if="player1Choice === 'paper.png'" src='./assets/paper.png' alt="Paper" />
          <img v-if="player1Choice === 'scissors.png'" src='./assets/scissor.png' alt="Scissors" />
          <img v-if="player1Choice === 'love.png'" src='./assets/love.png' alt="love" /> 
        </div>
      </div>

      <div class="computer">
        <h2>Player2</h2>
        <p class="score">Score: {{ player2Score }}</p>
        <div class="choice">
          <img v-if="!player2Choice" src="./assets/default.png" />
          <img v-if="player2Choice === 'rock.png'" src='./assets/rock.png' alt="Rock" />
          <img v-if="player2Choice === 'paper.png'" src='./assets/paper.png' alt="Paper" />
          <img v-if="player2Choice === 'scissors.png'" src='./assets/scissor.png' alt="Scissors" />
          <img v-if="player2Choice === 'love.png'" src='./assets/love.png' alt="love" />
        </div>
      </div>
    </div>

    <div class="choices">
      <button @click="playRandom" class="play-random-button">เป่ายิงฉุบ</button>
    </div>

    <div class="result">
      <button @click="resetGame" class="reset-button">เล่นใหม่</button>
      <p class="result-message">{{ resultMessage }}</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      player1Score: 0,
      player2Score: 0,
      resultMessage: '',
      player1Choice: '',
      player2Choice: '',
    };
  },
  methods: {
    play(player1Choice) {
      const choices = ['rock.png', 'paper.png', 'scissors.png', 'love.png']; 

      const player1ChoiceIndex = choices.indexOf(player1Choice);
      const player2ChoiceIndex = Math.floor(Math.random() * choices.length);

      const player2Choice = choices[player2ChoiceIndex];

      const player1ChoiceImage = player1Choice;
      const player2ChoiceImage = player2Choice;

      this.player1Choice = player1ChoiceImage;
      this.player2Choice = player2ChoiceImage;

      if (player1Choice === player2Choice) {
        this.resultMessage = "It's a tie!";
      } else if (
        (player1Choice === 'rock.png' && player2Choice === 'scissors.png') ||
        (player1Choice === 'paper.png' && player2Choice === 'rock.png') ||
        (player1Choice === 'scissors.png' && player2Choice === 'paper.png') ||
        (player1Choice === 'love.png') 
      ) {
        this.resultMessage = 'Player1 win!';
        this.player1Score++;
      } else {
        this.resultMessage = 'Player2 wins!';
        this.player2Score++;
      }
    },
    resetGame() {
      this.player1Score = 0;
      this.player2Score = 0;
      this.resultMessage = '';
      this.player1Choice = '';
      this.player2Choice = '';
    },
    playRandom() {
      const choices = ['rock.png', 'paper.png', 'scissors.png', 'love.png']; 
      const player1ChoiceIndex = Math.floor(Math.random() * choices.length);
      const player1Choice = choices[player1ChoiceIndex];
      this.play(player1Choice);
    },
  },
};
</script>




<style scoped>
#app {
  font-family: Arial, sans-serif;
  text-align: center;
  padding: 10px;
  background-color: #ffffff;
  color: #000000;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 100px;
}

.title {
  font-size: 36px;
  margin-top: 0px;
  color: #000000; 
}
.choice img {
  width: 150px; 
  height: 150px; 
}
.players {
  display: flex;
  justify-content: space-around;
  margin-top: 20px;
  width: 100%;
  margin-bottom: 40px;
}

.player,
.computer {
  text-align: center;
  background-color: #ffffff;
  color: #000000;
  border-radius: 8px;
  padding: 20px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  width: 45%; 
}

.score {
  font-size: 24px;
  margin-bottom: 10px;
}

.choices {
  display: flex;
  justify-content: space-around;
}


/* CSS */
button {
  appearance: none;
  background-color: transparent;
  border: 2px solid #1A1A1A;
  border-radius: 15px;
  box-sizing: border-box;
  color: #3B3B3B;
  cursor: pointer;
  display: inline-block;
  font-family: Roobert,-apple-system,BlinkMacSystemFont,"Segoe UI",Helvetica,Arial,sans-serif,"Apple Color Emoji","Segoe UI Emoji","Segoe UI Symbol";
  font-size: 16px;
  font-weight: 600;
  line-height: normal;
  margin: 0;
  min-height: 60px;
  min-width: 0;
  outline: none;
  padding: 16px 24px;
  text-align: center;
  text-decoration: none;
  transition: all 300ms cubic-bezier(.23, 1, 0.32, 1);
  user-select: none;
  -webkit-user-select: none;
  touch-action: manipulation;
  width: 100%;
  will-change: transform;
}

button:disabled {
  pointer-events: none;
}

button:hover {
  color: #fff;
  background-color: #1A1A1A;
  box-shadow: rgba(0, 0, 0, 0.25) 0 8px 15px;
  transform: translateY(-2px);
}

button:active {
  box-shadow: none;
  transform: translateY(0);
}
</style>