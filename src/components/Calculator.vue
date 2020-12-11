<template>
  <div class="calculator">
    <div class="display">{{ current || 0 }}</div>
    <button @click="clear" class="btn">C</button>
    <button @click="sign" class="btn">+/-</button>
    <button @click="percent" class="btn">%</button>
    <button @click="divide" class="btn operator">/</button>
    <button @click="append('7')" class="btn">7</button>
    <button @click="append('8')" class="btn">8</button>
    <button @click="append('9')" class="btn">9</button>
    <button @click="times" class="btn operator">X</button>
    <button @click="append('4')" class="btn">4</button>
    <button @click="append('5')" class="btn">5</button>
    <button @click="append('6')" class="btn">6</button>
    <button @click="minus" class="btn operator">-</button>
    <button @click="append('1')" class="btn">1</button>
    <button @click="append('2')" class="btn">2</button>
    <button @click="append('3')" class="btn">3</button>
    <button @click="plus" class="btn operator">+</button>
    <button @click="append('0')" class="zero btn">0</button>
    <button @click="dot" class="btn">.</button>
    <button @click="equal" class="btn operator">=</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      current: '',
      operator: null,
      previous: null,
      operatorClicked: null,
    }
  },
  methods: {
    clear() {
      this.current = '';
    },
    sign() {
      this.current = this.current.charAt(0) === '-' ? this.current.slice(1) : `-${this.current}`
    },
    percent() {
      this.current = `${parseFloat(this.current) / 100}`
    },
    append(number) {
      if (this.operatorClicked) {
        this.current = '';
        this.operatorClicked = false;
      }
      this.current = `${this.current}${number}`
    },
    dot() {
      if (!this.current.includes('.')) {
        this.append('.')
      }
    },
    setPrevious() {
      this.previous = this.current;
      this.operatorClicked = true;
    },
    divide() {
      this.operator = (a, b) => a / b;
      this.setPrevious();
    },
    times() {
      this.operator = (a, b) => a * b;
      this.setPrevious();
    },
    minus() {
      this.operator = (a, b) => a - b;
      this.setPrevious();
    },
    plus() {
      this.operator = (a, b) => a + b;
      this.setPrevious();
    },
    equal() {
      this.current = this.operator(parseFloat(this.previous), parseFloat(this.current)).toString();
      this.previous = null;
    }
  }
}
</script>

<style scoped>

.calculator {
  font-size: 40px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
  width: 400px;
  margin: auto;
}

.display {
  grid-column: 1 / 5;
  background-color: #333;
  color: white;
}

.zero {
  grid-column: 1 / 3;
}

.btn {
  background-color: #eee;
  border: 1px solid #333;
  font-size: 25px;
}

.operator {
  background-color: orange;
}

</style>
