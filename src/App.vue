<template>
  <div id="app">
    <Header />
    <Timer />
    <Checks />
  </div>
</template>

<script>
import Header from "./components/Header";
import Timer from "./components/Timer";
import Checks from "./components/Checks";
export default {
  name: "App",
  components: {
    Header,
    Timer,
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
