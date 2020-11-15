<template>
  <div class="check-container">{{ nada }}</div>
</template>

<script>
export default {
  data() {
    return {
      nada: "",
    };
  },
};
</script>

<style scoped>
.check-container {
  /* background-color: var(--primary-color); */
  color: var(--tertiary-color);

  /* padding-bottom: 2rem; */
  /* padding-top: 1rem; */
  /* display: flex; */
  /* flex-direction: row; */
  /* justify-content: space-around; */
  /* margin-bottom: 5rem; */
}
</style>
