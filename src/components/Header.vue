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
  align-items: center;
  padding-top: 0.5rem;
  padding-bottom: 1rem;
  background-color: var(--primary-color);
  color: var(--secondary-color);
}

.tomato {
  height: 4rem;
  margin-left: 50%;
  transform: translate(-230%);
}

h1 {
  font-size: 5rem;
  margin-left: -8.5rem;
}
</style>
