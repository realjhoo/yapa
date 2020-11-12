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
const FULL_DASH_ARRAY = 283;
const WARNING_THRESHOLD = 30; // set to 150 sec -> 2:30
const ALERT_THRESHOLD = 10; // set to 60 sec

const COLOR_CODES = {
  info: {
    color: "green",
  },
  warning: {
    color: "orange",
    threshold: WARNING_THRESHOLD,
  },
  alert: {
    color: "red",
    threshold: ALERT_THRESHOLD,
  },
};

const TIME_LIMIT = 90;

export default {
  data() {
    return {
      timePassed: 0,
      timerInterval: null,
      startStop: "Start",
    };
  },

  computed: {
    circleDasharray() {
      return `${(this.timeFraction * FULL_DASH_ARRAY).toFixed(0)} 283`;
    },

    formattedTimeLeft() {
      const timeLeft = this.timeLeft;
      const minutes = Math.floor(timeLeft / 60);
      let seconds = timeLeft % 60;

      if (seconds < 10) {
        seconds = `0${seconds}`;
      }

      return `${minutes}:${seconds}`;
    },

    timeLeft() {
      return TIME_LIMIT - this.timePassed;
    },

    timeFraction() {
      const rawTimeFraction = this.timeLeft / TIME_LIMIT;
      return rawTimeFraction - (1 / TIME_LIMIT) * (1 - rawTimeFraction);
    },

    remainingPathColor() {
      const { alert, warning, info } = COLOR_CODES;

      if (this.timeLeft <= alert.threshold) {
        return alert.color;
      } else if (this.timeLeft <= warning.threshold) {
        return warning.color;
      } else {
        return info.color;
      }
    },
  },

  watch: {
    timeLeft(newValue) {
      if (newValue === 0) {
        this.onTimesUp();
      }
    },
  },

  // mounted() {
  //   this.startTimer();
  // },

  methods: {
    onTimesUp() {
      clearInterval(this.timerInterval);
    },

    startTimer() {
      this.timerInterval = setInterval(() => (this.timePassed += 1), 1000);
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
  transform: scaleX(-1);
}

.countdown__circle {
  fill: none;
  stroke: none;
}

.countdown__path-elapsed {
  stroke-width: 3px;
  stroke: grey;
}

.countdown__path-remaining {
  stroke-width: 3px;
  stroke-linecap: round;
  transform: rotate(90deg);
  transform-origin: center;
  transition: 1s linear all;
  fill-rule: nonzero;
  stroke: currentColor;
}

.green {
  color: rgb(65, 184, 131);
}

.orange {
  color: orange;
}

.red {
  color: var(--tertiary-color);
}

.countdown__label {
  position: absolute;
  width: 300px;
  height: 300px;
  top: -15px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 48px;
  /* color: #fff; */
  font-family: "Syne Mono", monospace;
  font-size: 5rem;
  color: var(--secondary-color);
}

.work-break__label {
  position: absolute;
  display: flex;
  top: 170px;
  left: 50%;
  transform: translate(-50%);
  align-items: center;
  justify-content: center;
  /* width: 300px; */
  /* height: 300px; */
  font-family: "Syne", sans-serif;
  font-size: 3rem;
  background-color: pink;
}

button {
  font-size: 2rem;
}

.start-button {
  margin-left: 6rem;
  padding: 10px 20px;
  border-radius: 30px;
  font-size: 2rem;
  color: var(--primary-color);
  background-color: var(--secondary-color);
  font-weight: bold;
  outline: none;
}
</style>