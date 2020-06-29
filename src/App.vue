<template>
  <div id="app">
    <div id="buttons">
      <button class="start" @click="startTimer" v-if="!timer">Démarrer</button>
      <button class="pause" @click="stopTimer" v-if="timer">Arrêter</button>
      <button class="reset" @click="resetTimer" v-if="resetButton">
        Reset
      </button>
    </div>
    <div id="timer">
      <img alt="Tomate" class="tomate" src="./assets/tomate.png" />
      <div class="count">
        <p>{{ minutes }}</p>
        <span>:</span>
        <p>{{ seconds }}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  components: {},
  data() {
    return {
      timer: null,
      totalTime: 25 * 60,
      resetButton: false,
    };
  },
  methods: {
    startTimer: function() {
      this.timer = setInterval(() => this.countdown(), 1000);
      this.resetButton = true;
    },
    stopTimer: function() {
      clearInterval(this.timer);
      this.timer = null;
      this.resetButton = true;
    },
    resetTimer: function() {
      this.totalTime = 25 * 60;
      clearInterval(this.timer);
      this.timer = null;
      this.resetButton = false;
    },
    padTime: function(time) {
      return (time < 10 ? "0" : "") + time;
    },
    countdown: function() {
      if (this.totalTime >= 1) {
        this.totalTime--;
      } else {
        this.totalTime = 0;
        this.resetTimer();
      }
    },
  },
  // ========================
  computed: {
    minutes: function() {
      const minutes = Math.floor(this.totalTime / 60);
      return this.padTime(minutes);
    },
    seconds: function() {
      const seconds = this.totalTime - this.minutes * 60;
      return this.padTime(seconds);
    },
  },
};
</script>

<style>
body {
  margin: 0;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  width: 100%;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}

#buttons {
  position: absolute;
  top: 0;
}

#timer {
  position: relative;
}

.tomate,
.count {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}

.count {
  color: white;
  font-weight: bold;
  font-size: 4rem;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
