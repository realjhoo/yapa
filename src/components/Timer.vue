<template>
  <div class="timer-container">
    <radial-progress-bar
      :diameter="300"
      :time-remaining="timeRemaining"
      :work-break="workBreak"
      :completed-steps="completedSteps"
      :total-steps="totalSteps"
      :inner-stroke-color="innerStrokeColor"
    >
      <p class="time-remaining-text">{{ timeRemaining }}</p>
      <p class="work-break-text">{{ workBreak }}</p>
    </radial-progress-bar>
    <br />
    <button class="start-button" @click="startTimer">Start</button>
  </div>
</template>

// ***********************************
<script>
import RadialProgressBar from "vue-radial-progress";

// function xtest() {
// console.log("test");
// this.timeRemaining = 10;
// return 10;
// }

export default {
  data() {
    return {
      timeRemaining: "21:35",
      workBreak: "Work",
      totalSteps: 100,
      completedSteps: 0,
      innerStrokeColor: "#1f1f1f",
      timerCount: 30,
    };
  },
  methods: {
    start() {
      this.timeRemaining = "15:20";
      console.log("this works tho");
    },
    startTimer() {
      this.timeRemaining = setInterval(() => (this.completedSteps += 1), 1000);
    },
  },
  // computed: {
  //   xtest: function() {
  //     let y = 0;
  //     for (let i = 0; i < 100; i++) {
  //       // ********** CODE GOES HERE I THINK *******
  //       y++;
  //     }
  //     console.log("Test output: ", y);
  //     // this.countdown;
  //     return y;
  //   },
  // },

  components: {
    RadialProgressBar,
  },
};
// xtest();
</script>

<style scoped>
.timer-container {
  margin-top: 6rem;
  margin-bottom: 6rem;
  margin-left: 50%;
  transform: translate(-50%);
  /* background-color: blue; */
}

.time-remaining-text {
  font-family: "Syne Mono", monospace;
  font-size: 5rem;
  color: var(--secondary-color);
}

.work-break-text {
  font-size: 3rem;
  color: var(--secondary-color);
}

/* .start-button {
  margin-left: 6rem;
  padding: 10px 20px;
  border-radius: 30px;
  font-size: 2rem;
  color: var(--primary-color);
  background-color: var(--secondary-color);
  font-weight: bold;
  outline: none;
} */
</style>
