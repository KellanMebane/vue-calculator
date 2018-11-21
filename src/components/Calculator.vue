<template>
  <div class="calculator">
    <div class="display">{{left + operator + right}}</div>
    <a @click="clear('0')" class="btn">C</a>
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
    <a @click="append(0)" class="btn zero">0</a>
    <a @click="dot" class="btn">.</a>
    <a @click="evaluate()" class="btn operator">=</a>
  </div>
</template>

<script>
/* eslint-disable */

export default {
  name: "Calculator",

  data() {
    return {
      left: "0",
      right: "",
      operator: "",
      on: false
    };
  },

  methods: {
    clear(left) {
      this.left = left;
      this.right = "";
      this.operator = "";
      this.on = false; // on being true means we are operating on the right hand side
    },

    sign() {
      let current = this.on ? this.right : this.left;
      current = current.charAt(0) === "-" ? current.slice(1) : `-${current}`;

      if (this.on) {
        this.right = current;
      } else {
        this.left = current;
      }
    },

    percent() {
      if (this.on) {
        this.right = `${parseFloat(this.right) / 100}`;
        //if (this.rigt == 'NaN')
      } else {
        this.left = `${parseFloat(this.left) / 100}`;
      }
    },

    append(number) {
      let current = this.on ? this.right : this.left;

      if (current === "0" && number != ".") {
        current = `${number}`;
      } else {
        current = `${current + number}`;
      }

      if (this.on) {
        this.right = current;
      } else {
        this.left = current;
      }
    },

    dot() {
      let current = this.on ? this.right : this.left;
      current = current === "" ? current = "0" : current;
      current.indexOf(".") === -1 ? (current = `${current + "."}`) : {};
      if (this.on) {
        this.right = current;
      } else {
        this.left = current;
      }
    },

    op(operator) {
      if (this.operator.length === 0) {
        this.operator = operator;
        this.on = true;
      }
    },

    evaluate() {
      let result = "0";
      switch (this.operator) {
        case "+":
          result = `${parseFloat(this.left) + parseFloat(this.right)}`;
          this.clear(result);
          break;
        case "-":
          result = `${parseFloat(this.left) - parseFloat(this.right)}`;
          this.clear(result);
          break;
        case "x":
          result = `${parseFloat(this.left) * parseFloat(this.right)}`;
          this.clear(result);
          break;
        case "÷":
          result = `${parseFloat(this.left) / parseFloat(this.right)}`;
          this.clear(result);
          break;
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
