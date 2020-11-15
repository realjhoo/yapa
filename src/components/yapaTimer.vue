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

    <span class="countdown__label">{{ formattedTimeRemaining }}</span>
    <span class="work-break__label">{{ workBreak }}</span>
    <br />

    <button @click="startPomodoro" class="start-button">{{ startStop }}</button>
    <component :is="currentCheckState"></component>
  </div>
</template>

<script>
import Check0 from "./check0";
import Check1 from "./check1";
import Check2 from "./check2";
import Check3 from "./check3";
import Check4 from "./check4";

// set time params in seconds
const WORK_TIME = 1500; // 15min
const BREAK_TIME = 300; // 5min
const LONG_BREAK_TIME = 900; // 15min

let timeLimit = WORK_TIME;

const FULL_DASH_ARRAY = 283; // 283
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
    color: "white",
    threshold: ALERT_THRESHOLD,
  },
};

export default {
  components: {
    Check0,
    Check1,
    Check2,
    Check3,
    Check4,
  },
  data() {
    return {
      timeElapsed: 0,
      timerInterval: null,
      startStop: "Start",
      workBreak: null,
      pomodoro: 1,
      currentCheckState: "Check0",
      checkcount: 0,
    };
  },

  computed: {
    // ====================================================
    circleDasharray() {
      return `${(this.timeFraction * FULL_DASH_ARRAY).toFixed(0)} 283`;
    },

    // ====================================================
    formattedTimeRemaining() {
      const timeRemaining = this.timeRemaining;
      const minutes = Math.floor(timeRemaining / 60);
      let seconds = timeRemaining % 60;

      if (seconds < 10) {
        seconds = `0${seconds}`;
      }

      return `${minutes}:${seconds}`;
    },

    // ====================================================
    timeRemaining() {
      return timeLimit - this.timeElapsed;
    },

    // ====================================================
    timeFraction() {
      const rawTimeFraction = this.timeRemaining / timeLimit;
      return rawTimeFraction - (1 / timeLimit) * (1 - rawTimeFraction);
    },

    // ====================================================
    remainingPathColor() {
      const { alert, warning, info } = COLOR_CODES;

      if (this.timeRemaining <= alert.threshold) {
        return alert.color;
      } else if (this.timeRemaining <= warning.threshold) {
        return warning.color;
      } else {
        return info.color;
      }
    },
  },

  // ======================================================
  watch: {
    timeRemaining(newValue) {
      if (newValue === 0) {
        this.onTimesUp();
      }
    },
  },

  methods: {
    // ====================================================
    isOdd(num) {
      return num % 2 === 1; // true if odd false if even
    },

    // ====================================================
    startPomodoro() {
      //
      if (this.startStop === "Start") {
        this.startStop = "Stop";
        this.workBreak = "Work";
        this.pomodoro = 1;
        this.checkcount = 0;
        this.startTimer();
        //
      } else if (this.startStop === "Stop") {
        this.startStop = "Start";
        this.workBreak = null;
        this.timeElapsed = 0;
        timeLimit = WORK_TIME;
        this.pomodoro = 9; // triggers reset
        this.onTimesUp();
      }

      if (this.startStop === "Reset") {
        this.startStop = "Start";
        this.workBreak = null;
        this.pomodoro = 0;
        this.currentCheckState = "Check0";
      }
    },

    // ====================================================
    onTimesUp() {
      clearInterval(this.timerInterval);
      //
      this.pomodoro++;
      // *** WORK ODD ***
      if (this.isOdd(this.pomodoro)) {
        if (this.pomodoro <= 7) {
          this.setWork();
        }
        // *** COMPLETE ***
        if (this.pomodoro === 9) {
          this.setComplete();
        }
      }
      // *** BREAK EVEN ***
      if (!this.isOdd(this.pomodoro)) {
        if (this.pomodoro <= 6) {
          this.setBreak();
        }
        // *** LONG BREAK ***
        if (this.pomodoro === 8) {
          this.setRest();
        }
        if (this.pomodoro === 10) {
          // *** RESET ***
          this.resetCheck();
        }
      }
    },

    // ====================================================
    startTimer() {
      this.timerInterval = setInterval(() => (this.timeElapsed += 1), 1000);
    },

    // ======================================================
    setWork() {
      this.workBreak = "Work";
      this.timeElapsed = 0;
      timeLimit = WORK_TIME;
      this.startTimer();
    },

    // ======================================================
    setBreak() {
      this.checkcount++;
      this.currentCheckState = "Check" + this.checkcount;
      this.workBreak = "Break";
      this.timeElapsed = 0;
      timeLimit = BREAK_TIME;
      this.startTimer();
    },

    // ======================================================
    setRest() {
      this.checkcount++;
      this.currentCheckState = "Check" + this.checkcount;
      this.workBreak = "Rest";
      this.timeElapsed = 0;
      timeLimit = LONG_BREAK_TIME;
      this.startTimer();
    },

    // ======================================================
    setComplete() {
      this.pomodoro = 1;
      timeLimit = WORK_TIME;
      this.timeElapsed = 0;
      this.workBreak = "Complete";
      this.startStop = "Reset";
    },

    // ====================================================
    resetChecks() {
      this.currentCheckState = "Check0";
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
  margin-bottom: 7rem;
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
  fill: var(--tertiary-color);
  stroke: none;
}

.countdown__path-elapsed {
  stroke-width: 3px;
  stroke: black;
}

.countdown__path-remaining {
  stroke-width: 2px;
  stroke-linecap: round;
  transform: rotate(90deg);
  transform-origin: center;
  transition: 1s linear all;
  fill-rule: nonzero;
  stroke: currentColor;
}

.green {
  color: #41b882;
}

.orange {
  color: goldenrod;
}

.white {
  color: #fff;
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
  font-family: "Syne", sans-serif;
  font-size: 3rem;
}

.start-button {
  margin-left: 50%;
  transform: translate(-50%);
  padding: 10px 20px;
  border-radius: 30px;
  font-size: 2rem;
  color: var(--primary-color);
  background-color: var(--secondary-color);
  font-weight: bold;
  outline: none;
}
</style>
