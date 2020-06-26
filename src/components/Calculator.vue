<template>
  <div class="container">
    <div class="display">{{ display || 0 }}</div>

    <div @click="clear" class="operands">AC</div>
    <div @click="plusminus" class="operands">+/-</div>
    <div @click="percentage" class="operands">%</div>

    <div @click="divide" class="operands">/</div>
    <div @click="getDigit('7')" class="digits">7</div>
    <div @click="getDigit('8')" class="digits">8</div>
    <div @click="getDigit('9')" class="digits">9</div>

    <div @click="multiply" class="operands">*</div>
    <div @click="getDigit('4')" class="digits">4</div>
    <div @click="getDigit('5')" class="digits">5</div>
    <div @click="getDigit('6')" class="digits">6</div>

    <div @click="minus" class="operands">-</div>
    <div @click="getDigit('1')" class="digits">1</div>
    <div @click="getDigit('2')" class="digits">2</div>
    <div @click="getDigit('3')" class="digits">3</div>

    <div @click="add" class="operands">+</div>
    <div @click="getDigit('0')" class="zero digits">0</div>
    <div @click="dott" class="digits">.</div>
    <div @click="equal" class="operands">=</div>
  </div>
</template>

<script>
export default {
  name: "Calculator",

  data() {
    return {
      display: "",
      operatorClicked: false,
      operator: null,
      previousClick: null
    };
  },
  methods: {
    clear() {
      this.display = "";
      this.operator = null;
      this.previousClick = null;
    },
    getDigit(digit) {
      if (this.operatorClicked) {
        this.display = "";
        this.operatorClicked = false;
      }
      this.display += digit;
    },
    plusminus() {
      if (this.display != "") {
        this.display =
          this.display.charAt(0) === "-"
            ? this.display.slice(1)
            : `-${this.display}`;
      }
    },
    add() {
      this.operator = (a, b) => a + b;
      this.previousClick = this.display;
      this.operatorClicked = true;
    },
    percentage() {
      this.display = parseFloat(this.display / 100);
      this.previousClick = this.display;
      this.operatorClicked = true;
    },
    divide() {
      this.operator = (a, b) => a / b;
      this.previousClick = this.display;
      this.operatorClicked = true;
    },
    minus() {
      this.operator = (a, b) => a - b;
      this.previousClick = this.display;
      this.operatorClicked = true;
    },
    multiply() {
      this.operator = (a, b) => a * b;
      this.previousClick = this.display;
      this.operatorClicked = true;
    },
    dott() {
      // checks if dot decimal has been added before adding it
      if (this.display.indexOf(".") === -1) {
        this.display += ".";
      }
    },
    equal() {
      if (this.previousClick != null && this.display != "") {
        this.display = `${this.operator(
          parseFloat(this.previousClick),
          parseFloat(this.display)
        )}`;
        this.previousClick = null;
      }
    }
  }
};
</script>

<style scoped>
html,
body {
  background-color: black;
}

.container {
  font-weight: bold;
  color: white;
  display: grid;
  grid-template-rows: repeat(6, 0.5fr);
  grid-template-columns: repeat(4, 1fr);
  width: 100vw;
  height: 100vh;
}

.zero {
  grid-column: 1/3;
}

.display {
  padding: 30px;
  border: 1px solid;
  font-size: 2rem;
  grid-column: 1/5;
  text-align: right;
  color: white;
  background-color: #1c1c1c;
}

.operands,
.digits {
  padding: 30px;
  font-size: 1.5rem;
  border: 1px solid;
  text-align: center;
  transition: background-color 1s;
}

.operands {
  background-color: #ff9500;
}

.digits {
  background-color: #d4d4d2;
}

.operands:active,
.digits:active {
  background-color: rgb(151, 14, 14);
}
</style>
