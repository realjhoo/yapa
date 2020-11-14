<template>
  <div id="app">
    <Header />
    <YapaTimer />
    <!-- <Countdown /> -->
    <!-- <Timer /> -->
    <Checks />
  </div>
</template>

<script>
import Header from "./components/Header";
// import Timer from "./components/Timer";
// import Countdown from "./components/Countdown";
import Checks from "./components/Checks";
import YapaTimer from "./components/yapaTimer";
export default {
  name: "App",

  components: {
    Header,
    YapaTimer,
    // Timer,
    // Countdown,
    Checks,
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Syne&family=Syne+Mono&display=swap");

:root {
  --primary-color: #2c2c2c; /* Tucy Dark*/
  --secondary-color: #ce9e62; /* Rusted Gold */
  --accent-color: #4b6777; /* Rusted Copper */
  --tertiary-color: #c1432e; /* Rusted Red */
  --check-green: #41b882; /* Checkmark */
  --bez-curve: cubic-bezier(0.65, 0, 0.45, 1);
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
