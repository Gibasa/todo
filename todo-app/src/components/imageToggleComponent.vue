<template>
  <div class="image-toggle" @click="$emit('click')">
    <img v-if="mode === 'light'" src="../assets/img/icon-moon.svg" alt="moon" />
    <img v-if="mode === 'dark'" src="../assets/img/icon-sun.svg" alt="sun" />
  </div>
</template>

<script>
export default {
  name: 'ImageToggleComponent',
  props: {
    mode: String
  }
}
</script>

<style scoped>
.image-toggle {
  cursor: pointer;
}
</style>
