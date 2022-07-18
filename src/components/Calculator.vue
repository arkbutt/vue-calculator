<template>
  <v-container>
    <h1></h1>
    <div class="output">
      <div class="outputCalc">{{ calculatorValue || 0 }}</div>
    </div>
    <div class="buttons">
      <div
        class="button"
        v-for="n in btnArr"
        :key="n"
        :class="{ operator: ['C', '*', '/', '-', '+', '='].includes(n) }"
      >
        <div class="btn" @click="action(n)">
          {{ n }}
        </div>
      </div>
    </div>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      calculatorValue: "0",
      btnArr: [
        "C",
        "",
        "",
        "",
        "7",
        "8",
        "9",
        "/",
        "4",
        "5",
        "6",
        "*",
        "1",
        "2",
        "3",
        "-",
        "0",
        ",",
        "=",
        "+",
      ],
      operator: null,
      previousCalculatorValue: "",
      operators: {
        "+": this.add,
        "-": this.subtract,
        "*": this.multiply,
        "/": this.divide,
      },
    };
  },
  methods: {
    action(n) {
      if (!isNaN(n)) {
        this.calculatorValue += n + "";
      }
      if (n === "," && this.calculatorValue.indexOf(".") < 0) {
        this.calculatorValue += ".";
      }

      if (n === "C") {
        this.calculatorValue = "0";
      }
      if (["/", "*", "-", "+"].includes(n)) {
        this.operator = n;
        if (this.calculatorValue !== "0") {
          this.previousCalculatorValue = this.calculatorValue;
          this.calculatorValue = "0";
        }
      }

      if (n === "=") {
        this.calculatorValue = this.operators[this.operator](
          parseFloat(this.previousCalculatorValue),
          parseFloat(this.calculatorValue)
        );
      }
    },
    add(num1, num2) {
      return num1 + num2;
    },

    subtract(num1, num2) {
      return num1 - num2;
    },
    multiply(num1, num2) {
      return num1 * num2;
    },

    divide(num1, num2) {
      return num1 / num2;
    },
  },
};
</script>

<style>
h1 {
  margin-top: 100px;
  text-align: center;
}
.output {
  text-align: right;
  background-color: rgb(60, 159, 245);
  width: min(300px, 70%);
  margin: 2px auto;
  padding: 2px;
  border: 0.5px solid rgb(66, 138, 220);
  border-radius: 4px;
  box-shadow: 2.8px 2.8px 2.2px rgba(0, 0, 0, 0.008),
    6.7px 6.7px 5.3px rgba(0, 0, 0, 0.012),
    12.5px 12.5px 10px rgba(0, 0, 0, 0.015),
    22.3px 22.3px 17.9px rgba(0, 0, 0, 0.018),
    41.8px 41.8px 33.4px rgba(0, 0, 0, 0.022),
    100px 100px 80px rgba(0, 0, 0, 0.03);
}
.outputCalc {
  background-color: rgb(148, 207, 255);
  padding: 15px;
  border-radius: 3px;
}
.buttons {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
  width: min(300px, 70%);
  border: 0.2px solid rgb(66, 138, 220);
  border-radius: 4px;
  align-items: center;
  background-color: rgb(148, 207, 255);
  justify-content: center;
  margin: 10px auto;
  gap: 5px;
  box-shadow: 2.8px 2.8px 2.2px rgba(0, 0, 0, 0.008),
    6.7px 6.7px 5.3px rgba(0, 0, 0, 0.012),
    12.5px 12.5px 10px rgba(0, 0, 0, 0.015),
    22.3px 22.3px 17.9px rgba(0, 0, 0, 0.018),
    41.8px 41.8px 33.4px rgba(0, 0, 0, 0.022),
    100px 100px 80px rgba(0, 0, 0, 0.03);
}
.button {
  background-color: rgb(94, 161, 215);
  padding: 6px;
  border-radius: 3px;
  margin: 4px;
  font-size: 1.5em;
  font-weight: bold;
  color: #000;
  text-align: center;
  cursor: pointer;
  transition: all 0.2s ease-in-out;
}
.button:hover {
  background-color: rgb(66, 138, 220);
  color: #000;
}
.operator {
  background-color: rgb(87, 138, 197);
  color: #000;
}
.operator:hover {
  background-color: rgb(94, 158, 232);
}
</style>