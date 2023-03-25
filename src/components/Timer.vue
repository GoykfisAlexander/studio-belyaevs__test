<template>
  <div class="timer">
    <div class="time">
      {{
        timer === "h"
          ? new Date(
              seconds * 1000 + new Date().getTimezoneOffset() * 60 * 1000
            ).toLocaleTimeString()
          : timer === "m"
          ? `${Math.floor(seconds / 60)}:${seconds % 60}`
          : seconds
      }}
    </div>
    <div class="hr"></div>
    <Buttons
      v-bind:seconds="seconds"
      v-on:increment:seconds="incrementSeconds"
      v-on:reset:seconds="resetSeconds"
    />
  </div>
</template>

<script>
import Buttons from "./Buttons.vue";

export default {
  name: "Timer",
  data() {
    return {
      seconds: 0,
    };
  },
  props: {
    timer: {
      type: String,
    },
  },
  components: { Buttons },

  methods: {
    incrementSeconds() {
      this.seconds++;
    },
    resetSeconds() {
      this.seconds = 0;
    },
  },
};
</script>

<style>
.timer {
  display: grid;
  grid-template-rows: 48.5% 1% 48.5%;
  grid-auto-columns: 1fr;
  justify-content: center;
  font-size: 2vw;
}
.time {
  display: flex;
  justify-content: center;
  align-items: center;
}
.hr {
  border-bottom: 1px solid #9e9e9e;
}
</style>
