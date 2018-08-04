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
      operators: ['+', '-', '*', '/'],
      calculation: 0,
      operator: null,
      val1Num: 0,
      val2Num: 0,
      val1Str: '',
      val2Str: '',
    }
  },
  watch:  {
    val2Str: function() {
      return this.calculation = this.val2Str;
    },
    
    val1Str: function() {
      if (!this.val1Str.length) {
        return this.calculation = 0; 
      } else {
        return this.calculation = this.val1Str;
      }
    }
  },
  methods: {      
    setNum(val) {
      if (this.operator !== null) {
        this.val2Str += val;
      } else {
        this.val1Str += val;
      }
    },
    
    setOperator(val) {
      if (this.operator === null) {
          this.operator = val;
      } else {
        this.val1Num = this.doMath();
        this.val2Str = '';
        this.val1Str = this.val1Num.toString();
        this.operator = val;
      }  
    },
    
  }
}
</script>

<style lang="scss">
  * {
    font-size: 0.625rem;
  }
</style>
