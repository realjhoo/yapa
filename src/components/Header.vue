<template>
  <div class="container">
    <img src="./../assets/tomato.svg" alt="Pomodoro" class="tomato" />
    <h1>Y A P A</h1>
  </div>
</template>

<script>
export default {
  name: "Header",
};
</script>

<style>
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  padding-top: 1rem;
  padding-bottom: 0.1rem;
  color: var(--secondary-color);
}

.tomato {
  height: 4rem;
}

h1 {
  font-size: 5rem;
  padding-left: 1rem;
}
</style>
