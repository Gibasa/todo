<template>
  <main :class="mode">
    <div v-if="mode === 'light'">
      <listComponentLight :mode="mode" @update:mode="updateMode" />
    </div>
    <div v-if="mode === 'dark'">
      <listComponentDark :mode="mode" @update:mode="updateMode" />
    </div>
    <AtributionComponent />
  </main>
</template>
<script>
import listComponentLight from './components/listComponentLight.vue'
import listComponentDark from './components/listComponentDark.vue'
import AtributionComponent from './components/atributionComponent.vue'

export default {
  components: {
    listComponentDark,
    listComponentLight,
    AtributionComponent
  },
  data() {
    return {
      mode: 'light'
    }
  },
  methods: {
    updateMode(newMode) {
      this.mode = newMode
    }
  }
}
</script>

<style lang="scss" src="./assets/scss/main.scss"></style>
