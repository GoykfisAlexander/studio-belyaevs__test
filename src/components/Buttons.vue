<template>
  <div class="buttons">
    <div class="button" v-on:click="startTimer" v-show="!isRunning">►</div>

    <div class="button" v-show="isRunning" v-on:click="stopTimer">❚❚</div>

    <div class="button stop" v-on:click="resetTimer"></div>
  </div>
</template>
<script>
export default {
  name: "Buttons",
  props: {
    seconds: {
      type: Number,
      default: 0,
    },
  },
  data() {
    return {
      isRunning: false,
      timerId: null,
    };
  },
  methods: {
    startTimer() {
      this.isRunning = true;
      this.timerId = setInterval(() => {
        this.$emit("increment:seconds");
      }, 1000);
    },
    stopTimer() {
      this.isRunning = false;
      clearInterval(this.timerId);
    },
    resetTimer() {
      this.localSeconds = 0;
      this.isRunning = false;
      clearInterval(this.timerId);
      this.$emit("reset:seconds");
    },
  },
};
</script>
<style>
.buttons {
  display: flex;
  justify-content: space-evenly;
  align-items: center;
}
.button {
  cursor: pointer;
}
.stop {
  width: 2vw;
  height: 2vw;
  background-color: #9e9e9e;
}
.disabled {
  display: none;
}
</style>
