<template>
  <div class="calculator">
    <div class="display">
      <h1>{{ curr || 0 }}</h1>
    </div>
    <div class="main">
      <div @click="clear()" class="btn">AC</div>
      <div @click="neg()" class="btn">+/-</div>
      <div @click="percent()" class="btn">%</div>
      <div @click="divide()" class="btn operator">/</div>
      <div @click="append('7')" class="btn">7</div>
      <div @click="append('8')" class="btn">8</div>
      <div @click="append('9')" class="btn">9</div>
      <div @click="times()" class="btn operator">x</div>
      <div @click="append('4')" class="btn">4</div>
      <div @click="append('5')" class="btn">5</div>
      <div @click="append('6')" class="btn">6</div>
      <div @click="minus()" class="btn operator">-</div>
      <div @click="append('1')" class="btn">1</div>
      <div @click="append('2')" class="btn">2</div>
      <div @click="append('3')" class="btn">3</div>
      <div @click="add()" class="btn operator">+</div>
      <div @click="append('0')" class="btn zero">0</div>
      <div @click="dot()" class="btn">.</div>
      <div @click="equal()" class="btn operator">=</div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Calculator',
  data() {
    return {
      previous: null,
      curr: "",
      operator: null,
      operatorClicked: false,
    }
  },
  methods: {
    clear() {
      this.curr = "";
    },
    neg() {
      this.curr = this.curr.charAt(0) === "-" ? this.curr.slice(1) : `-${this.curr}`;
    },
    percent() {
      this.curr = `${parseFloat(this.curr) / 100}`;
    },
    append(number) {
      if(this.operatorClicked) {
        this.curr = "";
        this.operatorClicked = false;
      }
      this.curr = `${this.curr}${number}`;
    },
    dot() {
      if (this.curr.indexOf('.') === -1) {
        this.append('.');
      }
    },
    divide() {
      this.operator = (a, b) => a / b;
      this.previous = this.curr;
      this.operatorClicked = true;
    },
    times() {
      this.operator = (a, b) => a * b;
      this.previous = this.curr;
      this.operatorClicked = true;
    },
    minus() {
      this.operator = (a, b) => a - b;
      this.previous = this.curr;
      this.operatorClicked = true;
    },
    add(){
      this.operator = (a, b) => a + b;
      this.previous = this.curr;
      this.operatorClicked = true;
    },
    equal() {
      this.curr = `${this.operator(
        parseFloat(this.previous),
        parseFloat(this.curr)
      )}`;
      this.previous = null;
    }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .calculator {
    width: 40%;
    margin: 0 auto;
    margin-top: 100px;
  }
  .display {
    height: 100px;
    text-align: right;
    background-color: #333;
    color: white;
    font-size: 40px;
    border-radius: 3px;
    padding-top: 8px;
    padding-right: 20px;
    border: 1px solid #999;
  }
  .main {
    display: flex;
    flex-wrap: wrap;
  }

  .btn {
    width: calc(100% / 4);
    height: 100px;
    border: 1px solid #999;
    text-align: center;
    border-radius: 3px;
    padding-top: 30px;
    font-size: 40px;
    color: #333;
    cursor: pointer;
  }

  .btn:active {
     transform: scale(0.95);
  }

  .operator {
    background-color: orange;
    color: white;
  }

  .zero {
    width: 50%;
  }
</style>
