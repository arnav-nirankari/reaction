<template>
  <div class="wrapper">
    <div id="blocky">
      <button
        v-if="showBlock"
        @click="stopTimer"
        id="movebtn"
        class="btn"
        :style="{
          position: 'absolute',
          left: leftPosition,
          top: topPosition,
        }"
      >
        Click Me
      </button>
    </div>
  </div>
</template>

<script>
import { VueScreenSizeMixin } from "vue-screen-size";
var moveBtn = document.getElementById("#movebtn");
console.log(moveBtn);
export default {
  props: ["delay"],

  mixins: [VueScreenSizeMixin],

  data() {
    return {
      showBlock: false,
      timer: null,
      reactionTime: 0,
      leftPosition: 0,
      topPosition: 0,
      h: window.innerHeight,
      translate: null,

      // block: document.getElementById("blocky"),
    };
  },

  beforeMount() {
    this.leftPosition = 10 + Math.random() * 75 + "%";
    this.topPosition = 10 + Math.random() * 75 + "%";

    // console.log(moveBtn);
    // moveBtn.style.transform(-50 + "%", -50 + "%");
    // this.translate = translate(-this.leftPosition, -this.topPosition);
  },

  mounted() {
    //console.log("component mounted");
    setTimeout(() => {
      this.showBlock = true;

      // console.log(this.block.style);
      // block.style.top = Math.floor(Math.random() * 100) + "px";
      this.startTimer();
    }, this.delay);
  },
  methods: {
    startTimer() {
      this.timer = setInterval(() => {
        this.reactionTime += 10;
      }, 10);
    },

    move() {},

    stopTimer() {
      clearInterval(this.timer);
      // console.log(e);
      // console.log(this.reactionTime);
      this.$emit("end", this.reactionTime);
    },
  },
};
</script>

<style>
#blocky {
  width: 100vw;
  height: 100vh;
  background: #ffffff;
  color: white;
  text-align: center;
  /* padding: 100px 0;
  margin: 40px auto; */
  position: absolute;
  left: 0;
  right: 0;
  top: 0;
  bottom: 0;
  display: flex;
  align-items: center;
  justify-content: center;
}
button.btn {
  padding: 3% 5%;
  /* width: 150px; */
  margin: 0;
  display: inline-block;
}
/* .wrapper {
  position: relative;
  height: 100vh;
  width: 100vh;
  overflow: hidden;
} */
</style>