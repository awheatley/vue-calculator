<template>
  <div id="app">
    <p class="calculation">{{ calculation }}</p>
    <Buttons :buttons="buttons" :operators="operators" />
  </div>
</template>

<script>
import Buttons from './components/Buttons.vue'

export default {
  name: 'app',
  components: {
    Buttons
  },
  data() {
    return {
      buttons: [1, 2, 3, 4, 5, 6, 7, 8, 9, 0],
      operators: ['+', '-', '*', '/']
    }
  }
}
</script>

<style lang="scss">
  * {
    font-size: 0.625rem;
  }
</style>
