<template>
  <div class="calculator">
    <div class="display">{{current}}</div>
    <a @click="clear" class="btn">C</a>
    <a @click="sign" class="btn">+/-</a>
    <a @click="percent" class="btn">%</a>
    <a @click="op('÷')" class="btn operator">÷</a>
    <a @click="append(7)" class="btn">7</a>
    <a @click="append(8)" class="btn">8</a>
    <a @click="append(9)" class="btn">9</a>
    <a @click="op('x')" class="btn operator">x</a>
    <a @click="append(4)" class="btn">4</a>
    <a @click="append(5)" class="btn">5</a>
    <a @click="append(6)" class="btn">6</a>
    <a @click="op('-')" class="btn operator">-</a>
    <a @click="append(1)" class="btn">1</a>
    <a @click="append(2)" class="btn">2</a>
    <a @click="append(3)" class="btn">3</a>
    <a @click="op('+')" class="btn operator">+</a>
    <a @click="addZero()" class="btn zero">0</a>
    <a @click="dot" class="btn">.</a>
    <a @click="evaluate" class="btn operator">=</a>
  </div>
</template>

<script>
/* eslint-disable */

// [TODO] second number can't have decimals yet
// [TODO] sign will be read as an operator currently

export default {
  name: "Calculator",
  data() {
    return {
      current: "0",
      operator: "",
      done: false
    };
  },
  methods: {
    clear() {
      this.current = "0";
      this.operator = "";
      this.done = "";
    },

    sign() {
      this.current =
        this.current.charAt(0) === "-"
          ? this.current.slice(1)
          : `-${this.current}`;
    },

    percent() {
      this.current = `${parseFloat(this.current) / 100}`;
    },

    append(number) {
      if (this.current === "0" && number != ".") {
        this.current = `${number}`;
      } else if (this.done && this.operator.length != 1 && number != ".") {
        this.current = `${number}`;
      } else {
        this.current = `${this.current + number}`;
      }

      this.done = false;
    },

    dot() {
      this.current.indexOf(".") === -1 ? this.append(".") : {};
    },

    addZero() {
      this.current === "0" && this.current.length === 1
        ? this.current
        : this.append(0);
    },

    op(operator) {
      if (this.operator.length === 1) {
      } else if (this.current != "0") {
        this.operator = operator;        
        this.append(operator);
      }
    },

    evaluate() {
      if (this.operator.length === 1) {
        var nums = this.current.split(this.operator);

        switch (this.operator) {
          case "+":
            this.current = `${parseFloat(nums[0]) + parseFloat(nums[1])}`;
            break;
          case "-":
            this.current = `${parseFloat(nums[0]) - parseFloat(nums[1])}`;
            break;
          case "÷":
            this.current = `${parseFloat(nums[0]) / parseFloat(nums[1])}`;
            break;
          case "x":
            this.current = `${parseFloat(nums[0]) * parseFloat(nums[1])}`;
            break;
        }

        this.operator = "";
        this.done = true;
      }
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.calculator {
  width: 400px;
  margin: 0 auto;
  font-size: 40px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
}

.btn {
  background-color: #32495d;
  border: 1px solid #41b783;
}

.display {
  grid-column: 1 / 5;
  background-color: #673ab7;
  color: #dddddd;
}

.operator {
  background-color: dimgrey;
}

.zero {
  grid-column: 1 / 3;
}

a {
  color: #eeeeee;
}
</style>
