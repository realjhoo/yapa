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
  </div>
</template>

<script>
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
    color: "red",
    threshold: ALERT_THRESHOLD,
  },
};

//  sets the initial time in seconds
const TIME_LIMIT = 20; //25min = 1500s

export default {
  data() {
    return {
      timeElapsed: 0,
      timerInterval: null,
      startStop: "Start",
      workBreak: null,
      pomodoro: 1,
      checky: false,
    };
  },

  computed: {
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
      return TIME_LIMIT - this.timeElapsed;
    },

    // ====================================================
    timeFraction() {
      const rawTimeFraction = this.timeRemaining / TIME_LIMIT;
      return rawTimeFraction - (1 / TIME_LIMIT) * (1 - rawTimeFraction);
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

  watch: {
    timeRemaining(newValue) {
      if (newValue === 0) {
        this.onTimesUp();
      }
    },
  },

  // mounted() {
  //   this.startTimer();
  // },

  methods: {
    // ====================================================
    isOdd(num) {
      return num % 2 === 1;
    },
    // ====================================================
    startPomodoro() {
      // make sure label says "Work" when we start
      // if (this.pomodoro === 1) {
      //   this.workBreak = "Work";
      // }
      if (this.startStop === "Start") {
        this.startStop = "Stop";
        this.workBreak = "Work";
        this.startTimer();
      } else {
        // reset stuff
        this.startStop = "Start";
        this.workBreak = null;
        this.pomodoro = 9;
        this.onTimesUp();
        this.timeElapsed = 0;
        // set timer to 25m
      }
    },

    // ====================================================
    onTimesUp() {
      clearInterval(this.timerInterval);
      //
      this.pomodoro++;
      // console.log("checky: ", this.checky);
      // if (this.checky == false) {
      // this.checky = true;
      // console.log(this.checky);
      // this.checkOrNoCheck = "checked";
      // }

      // console.log(this.pomodoro);
      // if pomo is odd
      if (this.isOdd(this.pomodoro)) {
        if (this.pomodoro <= 7) {
          this.workBreak = "Work";
          // -- set timer to 25min
          // -- add a check
          // ---- cuz if that works, the svg will obviously work
          // ---- should I move button text etc to here?
          // -- startTimer()
        }
        // if pomo = 9, we're done
        if (this.pomodoro === 9) {
          this.pomodoro = 1;
          // -- timer to 25
          this.workBreak = "Complete";
          this.startStop = "Start";
          // -- dont restart the timer tho
          // ***** HOW CHANGE VALUE IN DIFFERENT COMPONENT???
        }
      }
      // if pomo is even -> BREAK
      if (!this.isOdd(this.pomodoro)) {
        console.log("???");
        if (this.pomodoro <= 6) {
          this.workBreak = "Break";
          // -- set timer to 5 min
          // -- add a check
          // -- startTimer()
        }
        // if pomo = 8 -> LONG BREAK
        if (this.pomodoro === 8) {
          this.workBreak = "Rest";
          // -- timer to 15
          // -- add a check
          // -- startTimer()
        }
      }
      // if pomo = 10 -> reset for another cycle
      if (this.pomodoro === 10) {
        // *** RESET ***
        this.workBreak = null;
        // timer to 25
        // remove checks
      }
    },

    // ====================================================
    startTimer() {
      this.timerInterval = setInterval(() => (this.timeElapsed += 1), 1000);
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
  /* fill: none; */
  fill: var(--tertiary-color);
  stroke: none;
  /* stroke: black; */
}

.countdown__path-elapsed {
  stroke-width: 3px;
  /* stroke: grey; */
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

.red {
  color: darkred;
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
  /* background-color: pink; */
}

/* button {
  font-size: 2rem;
} */

.start-button {
  /* margin-left: 6rem; */
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
