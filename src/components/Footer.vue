<template>
  <div>{{ footer }}</div>
</template>

<script>
export default {
  data() {
    return {
      footer: "Tomato icon by DinosoftLabs - flaticon.com",
    };
  },
};
</script>

<style scoped>
div {
  position: absolute;
  bottom: 5px;
  left: 50%;
  transform: translate(-50%);
  font-size: 0.6rem;
  color: var(--secondary-color);
}
</style>
