<template>
  <div class="container">
    <div class="result">
      {{  colculatorValue || 0  }}
    </div>
    <div class="button__pack">
      <div class="button" v-for="n in colculatorElements" :key="n" :class="{
        'green': ['C', '*', '/', '-', '+', '%', '='].includes(n)
      }" @click="action(n)">

        {{  n  }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Colculator',


  data() {
    return {
      colculatorValue: '',
      colculatorElements: ['C', '*', '/', '-', '7', '8', '9', '+', '4', '5', '6', '%', '1', '2', '3', '=', '0', '.'],
      operator: null,
      previousCalculatorValue: ''
    }
  },

  methods: {
    action(n) {
      if (!isNaN(n) || n === '.') {
        this.colculatorValue += n + ''
      } else if (n === 'C') {
        this.colculatorValue = ''
      } else if (n === '%') {
        this.colculatorValue = this.colculatorValue / 100 + ''
      } else if (['/', '*', '-', '+'].includes(n)) {
        this.operator = n;
        this.previousCalculatorValue = this.colculatorValue
        this.colculatorValue = ''
      } else if (n === '=') {
        this.colculatorValue = eval(
          this.previousCalculatorValue + this.operator + this.colculatorValue
        )
        this.previousCalculatorValue = '',
          this.operator = null
      }
    }
  }
}


</script>


<style scoped lang="scss">
.container {
  max-width: 300px;
  margin: 50px auto;
  background: #234;
  padding: 15px;
  align-items: center;

}

.result {
  text-align: right;
  margin: 0 20px;
  border-radius: 3px;
  padding: 15px 15px;
  font-weight: bold;
  color: #fff;
  background-color: #31475e;


}

.button__pack {
  margin: 10px 20px;
  display: flex;
  flex-wrap: wrap;

}

.button {
  cursor: pointer;
  display: flex;
  border-radius: 3px;
  background-color: #31475e;
  width: 60px;
  height: 40px;
  margin: 2.5px;
  align-items: center;
  justify-content: center;
  color: #fff;
  transition: all .2s;

  &.green {
    background-color: #3fb984;
  }


  &:hover {
    background-color: #3d5875;
  }


}

.lead {}
</style>
