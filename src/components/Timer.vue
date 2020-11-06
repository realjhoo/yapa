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
    <button class="start-button">Start</button>
  </div>
</template>

<script>
import RadialProgressBar from "vue-radial-progress";

export default {
  data() {
    return {
      timeRemaining: "21:39",
      workBreak: "Work",
      totalSteps: 100,
      completedSteps: 50,
      innerStrokeColor: "#1f1f1f",
    };
  },

  components: {
    RadialProgressBar,
  },
};
</script>

<style>
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

.start-button {
  margin-left: 6rem;
  padding: 10px 20px;
  border-radius: 30px;
  font-size: 2rem;
  color: var(--primary-color);
  background-color: var(--secondary-color);
  font-weight: bold;
}
</style>
