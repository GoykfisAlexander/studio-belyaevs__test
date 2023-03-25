<template>
  <Timer v-for="timer of timers" v-bind:timer="timer" />

  <div class="Add" v-on:click="addTimer">+</div>
</template>

<script>
import Timer from "./components/Timer.vue";

export default {
  name: "App",

  data() {
    return {
      timers: ["h", "m", "s"],
      lastKeyPressed: "h",
    };
  },
  components: {
    Timer,
  },
  mounted() {
    alert(
      "для добавления таймера используйте латинские буквы на клавиатуре - 'H M S' и кнопку добавить."
    );

    window.addEventListener("keydown", this.handleKeyDown);
  },
  beforeUnmount() {
    window.removeEventListener("keydown", this.handleKeyDown);
  },
  methods: {
    addTimer() {
      this.timers.push(this.lastKeyPressed);
    },
    handleKeyDown(event) {
      if (/[hsmрьы]/i.test(event.key)) {
        let key = event.key.toLowerCase();
        switch (key) {
          case "р":
            key = "h";
            break;
          case "ь":
            key = "m";
            break;
          case "ы":
            key = "s";
            break;
        }
        this.lastKeyPressed = key;
      }
    },
  },
};
</script>

<style>
body {
  margin: 0 0 0 0;
}
body div {
  background: #696969;
  color: #9e9e9e;
}

#app {
  background: #353638;
  width: 100vw;
  height: 100vh;
  display: grid;
  grid-template-columns: 18% 18% 18%;
  grid-auto-rows: 10vw;
  justify-content: center;
  align-content: center;
  grid-gap: 10vmin;
}
@media (max-width: 1024px) {
  #app {
    grid-template-columns: 25% 25%;
    grid-auto-rows: 12.5vw;
  }
}
@media (max-width: 768px) {
  #app {
    grid-template-columns: 55%;
    grid-auto-rows: 30vw;
  }
}
.Add {
  display: grid;
  justify-content: center;
  align-items: center;
  font-size: 3vw;
  cursor: pointer;
}
</style>
