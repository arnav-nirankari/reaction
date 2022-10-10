<template>
  <h1>Ninja Reaction Timer</h1>
  <div @click="rules" class="dd-button">How to play</div>
  <div v-if="showRules">
    <h5>
      - After you click the play button, a green box will randomly appear on the
      screen after a random delay.
    </h5>
    <h5>- Click on the box as soon as possible.</h5>
  </div>
  <br />
  <button @click="start" :disabled="isPlaying">Play</button>
  <ColorBlock v-if="isPlaying" :delay="delay" @end="endGame" />
  <MyResults v-if="showResults" :score="score" />
</template>

<script>
import ColorBlock from "./components/ColorBlock.vue";
import MyResults from "./components/MyResults.vue";

export default {
  name: "App",
  components: { ColorBlock, MyResults },
  data() {
    return {
      isPlaying: false,
      delay: 0,
      score: null,
      showResults: false,
      showRules: false,
    };
  },

  methods: {
    start() {
      this.isPlaying = true;
      this.delay = 500 + Math.random() * 5000;
      this.showResults = false;
    },

    endGame(reactionTime) {
      this.showResults = true;
      this.score = reactionTime;
      this.isPlaying = false;
      this.showRules = false;
    },

    rules() {
      this.showRules = !this.showRules;
    },
  },
};
</script>

<style>
* {
  box-sizing: border-box;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
button {
  background: #0faf87;
  color: white;
  border: none;
  padding: 8px 16px;
  border-radius: 4px;
  font-size: 16px;
  letter-spacing: 1px;
  cursor: pointer;
  margin: 10px;
}
button[disabled] {
  opacity: 0.2;
  cursor: not-allowed;
}

.dd-button {
  display: inline-block;
  border: 1px solid gray;
  border-radius: 4px;
  padding: 6px 14px 6px 14px;
  background-color: #ffffff;
  cursor: pointer;
  white-space: nowrap;
}

.dd-button:hover {
  background-color: #eeeeee;
}
/* .arrow {
  border: solid black;
  border-width: 0 3px 3px 0;
  display: inline-block;
  padding: 3px;
  transform: rotate(45deg);
  -webkit-transform: rotate(45deg);
} */
</style>
