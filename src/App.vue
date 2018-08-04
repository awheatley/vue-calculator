<template>
  <div id="app">
    <p class="calculation">{{ calculation }}</p>
    <Buttons :buttons="buttons" 
            :operators="operators" 
            v-on:setNum="setNum($event)" 
            v-on:setOperator="setOperator($event)" 
            v-on:doMath="doMath()" 
            v-on:clear="clear()" />
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
    
    doMath() {
      this.val1Num = parseFloat(this.val1Str);
      this.val2Num = parseFloat(this.val2Str);
      
      switch(this.operator) {
        case '+':
          return this.calculation = this.findSum(this.val1Num, this.val2Num);
          
        case '-':
          return this.calculation = this.findDifference(this.val1Num, this.val2Num);
          
        case '*':
          return this.calculation = this.findProduct(this.val1Num, this.val2Num);
          
        case '/':
          return this.calculation = this.findQuotient(this.val1Num, this.val2Num);
      }
    },
    
    clear() {
      this.calculation = 0;
      this.val1Str = '';
      this.val2Str = '';
      this.operator = null;
    },
    
    findSum(a, b) {
      return  a + b;
    },
    
    findDifference(a, b) {
      return  a - b;
    },
    
    findProduct(a, b) {
      return  a * b;
    },
  
    findQuotient(a, b) {
      return  a / b;
    }
  }
}
</script>

<style lang="scss">
  * {
    font-size: 0.625rem;
  }
</style>
