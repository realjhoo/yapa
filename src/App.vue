<template>
  <div id="app">
    <Header />
    <Timer />
    <Countdown />
    <Checks />
  </div>
</template>

<script>
import Header from "./components/Header";
import Timer from "./components/Timer";
import Countdown from "./components/Countdown";
import Checks from "./components/Checks";
export default {
  name: "App",

  components: {
    Header,
    Timer,
    Countdown,
    Checks,
  },

  // computed: {
  //   timeLeft() {
  //     return this.timeLimit - this.timePassed;
  //   },
  //   formattedTimeLeft() {
  //     const timeLeft = this.timeLeft;
  //     // The largest round integer less than or equal
  //     //   to the result of time divided being by 60.
  //     const minutes = Math.floor(timeLeft / 60);
  //     // Seconds are the remainder of the time divided
  //     //   by 60 (modulus operator)
  //     let seconds = timeLeft % 60;
  //     // If the value of seconds is less than 10,
  //     //   then display seconds with a leading zero
  //     if (seconds < 10) {
  //       seconds = `0${seconds}`;
  //     }
  //     // The output in MM:SS format
  //     return `${minutes}:${seconds}`;
  //   },
  // },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Syne&family=Syne+Mono&display=swap");

:root {
  --primary-color: #2c2c2c; /* Tucy Dark*/
  --secondary-color: #ce9e62; /* Rusted Gold */
  --accent-color: #4b6777; /* Rusted Copper */
  --tertiary-color: #c1432e; /* Rusted Red */
}

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

#app {
  font-family: "Syne", sans-serif;
  margin: 0;
  padding: 0;
  background-color: var(--primary-color);
}
</style>
