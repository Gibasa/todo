<template>
  <div class="attribution">
    Challenge by
    <a href="https://www.frontendmentor.io?ref=challenge" target="_blank">Frontend Mentor</a>. Coded
    by <a href="#">Gilberto Sá</a>.
  </div>
</template>

<script>
export default{
  name: 'AtributionComponent'
}
</script>

<style lang="scss" scoped>
.attribution {
  font-size: 11px;
  text-align: center;
  position: fixed;
  z-index: 1;
  bottom: 0;
  padding-bottom: 10px;
  color: hsl(235, 19%, 35%);
  a {
    color: hsl(228, 45%, 44%);
  }
}
</style>
