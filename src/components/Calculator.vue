<template>
  <div class="calculator">
    <div class="display">{{ result || 0 }}</div>
    <div class="btn clear" @click="clear">c</div>
    <div class="btn operator" @click="percentage">%</div>
    <div class="btn" @click="append(7)">7</div>
    <div class="btn" @click="append(8)">8</div>
    <div class="btn" @click="append(9)">9</div>
    <div class="btn operator" @click="divide">/</div>
    <div class="btn" @click="append(4)">4</div>
    <div class="btn" @click="append(5)">5</div>
    <div class="btn" @click="append(6)">6</div>
    <div class="btn operator" @click="multiply">*</div>
    <div class="btn" @click="append(1)">1</div>
    <div class="btn" @click="append(2)">2</div>
    <div class="btn" @click="append(3)">3</div>
    <div class="btn operator" @click="subtract">-</div>
    <div class="btn" @click="append(0)">0</div>
    <div class="btn" @click="dot">.</div>
    <div class="btn operator" @click="equal">=</div>
    <div class="btn operator" @click="sum">+</div>
  </div>
</template>

<script>
export default {
  // eslint-disable-next-line
  name: "Calculator",
  props: {
    msg: String,
  },
  data() {
    return {
      result: "",
      prev: null,
      operator: null,
      operatorClick: false,
    };
  },
  methods: {
    clear() {
      this.result = "";
    },
    percentage() {
      this.result = parseFloat(this.result) / 100;
    },
    append(number) {
      if (this.operatorClick) {
        this.result = "";
        this.operatorClick = false;
      }
      this.result = this.result + number;
    },
    dot() {
      if (this.result.indexOf(".") === -1) {
        this.append(".");
      }
    },
    divide() {
      this.operator = (a, b) => b / a;
      this.setPrev();
    },
    multiply() {
      this.operator = (a, b) => a * b;
      this.setPrev();
    },
    subtract() {
      this.operator = (a, b) => b - a;
      this.setPrev();
    },
    sum() {
      this.operator = (a, b) => a + b;
      this.setPrev();
    },
    equal() {
      this.result = this.operator(
        parseFloat(this.result),
        parseFloat(this.prev)
      );
      this.prev = null;
    },
    setPrev() {
      this.prev = this.result;
      this.operatorClick = true;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
* {
  background-color: #111;
}
.calculator {
  width: 400px;
  margin: 0 auto;
  font-size: 40px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(auto, auto);
  border: 20px groove #999;
}
.display {
  grid-column: 1/5;
  background-color: #333;
  color: #fff;
  text-align: right;
  padding: 20px;
}
.clear {
  grid-column: 1/4;
}
.btn {
  padding: 10px;
  background-color: #fafafa;
  cursor: pointer;
  border: 1px solid #999;
}
.operator {
  color: red;
}
.btn:active {
  background-color: #777;
  color: #fff;
}
</style>
