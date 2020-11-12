<template>
  <div class="countdown radial-container">
    <svg
      class="countdown__svg"
      viewBox="0 0 100 100"
      xmlns="http://www.w3.org/2000/svg"
    >
      <g class="countdown__circle">
        <circle class="countdown__path-elapsed" cx="50" cy="50" r="45"></circle>
        <path
          :stroke-dasharray="circleDasharray"
          class="countdown__path-remaining"
          :class="remainingPathColor"
          d="
            M 50, 50
            m -45, 0
            a 45,45 0 1,0 90,0
            a 45,45 0 1,0 -90,0
          "
        ></path>
      </g>
    </svg>
    <span class="countdown__label">{{ formattedTimeLeft }}</span>
    <span class="work-break__label">Work</span>
    <br />
    <button @click="startTimer" class="start-button">{{ startStop }}</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      timeElapsed: 0,
      timeInterval: null,
      startStop: "Start",
    };
  },

  computed: {},

  methods: {
    startTimer() {
      console.log("Hello World!");
    },
  },
};
</script>

<style scoped>
.radial-container {
  color: var(--secondary-color);
  background-color: var(--primary-color);
  margin-left: 50%;
  transform: translate(-50%);
}

.countdown {
  position: relative;
  width: 300px;
  height: 300px;
}

.countdown__svg {
  /* transform: scaleX(-1); */
}

.countdown__circle {
  fill: none;
  /* stroke: none; */
}

.countdown__path-elapsed {
  /* stroke-width: 3px; */
  stroke: grey;
}

.countdown__path-remaining {
  /* stroke-width: 3px; */
  /* stroke-linecap: round; */
  transform: rotate(90deg);
  transform-origin: center;
  /* transition: 1s linear all; */
  /* fill-rule: nonzero; */
  stroke: currentColor;
}

.green {
  /* color: rgb(65, 184, 131); */
}

.orange {
  /* color: orange; */
}

.red {
  /* color: var(--tertiary-color); */
}

.countdown__label {
  position: absolute;
  width: 300px;
  height: 300px;
  top: -15px;
  /* display: flex; */
  /* align-items: center; */
  /* justify-content: center; */
  /* font-size: 48px; */
  /* font-family: "Syne Mono", monospace; */
  /* font-size: 5rem; */
  /* color: var(--secondary-color); */
}

.work-break__label {
  /* position: absolute; */
  /* display: flex; */
  /* top: 50px; */
  /* align-items: center; */
  /* justify-content: center; */
  /* width: 300px; */
  /* height: 300px; */
  /* font-family: "Syne", sans-serif; */
  /* font-size: 3rem; */
}

.start-button {
  /* margin-left: 6rem; */
  /* padding: 10px 20px; */
  /* border-radius: 30px; */
  /* font-size: 2rem; */
  /* color: var(--primary-color); */
  /* background-color: var(--secondary-color); */
  /* font-weight: bold; */
  /* outline: none; */
}
</style>
