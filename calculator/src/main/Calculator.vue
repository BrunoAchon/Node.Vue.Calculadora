<template>
  <div class="calculator">
    <Display :value="displayValue" />
    <Button label="AC" @onClick="clearMemory" triple />
    <Button label="/" @onClick="setOperation" operation />
    <Button label="7" @onClick="addDigit" />
    <Button label="8" @onClick="addDigit" />
    <Button label="9" @onClick="addDigit" />
    <Button label="*" @onClick="setOperation" operation />
    <Button label="4" @onClick="addDigit" />
    <Button label="5" @onClick="addDigit" />
    <Button label="6" @onClick="addDigit" />
    <Button label="-" @onClick="setOperation" operation />
    <Button label="1" @onClick="addDigit" />
    <Button label="2" @onClick="addDigit" />
    <Button label="3" @onClick="addDigit" />
    <Button label="+" @onClick="setOperation" operation />
    <Button label="0" @onClick="addDigit" double />
    <Button label="." @onClick="addDigit" />
    <Button label="=" @onClick="setOperation" operation />
  </div>
</template>

<script>
import Display from "../components/Display.vue";
import Button from "../components/Button.vue";

export default {
  name: "calculator-item",

  data: function () {
    return {
      displayValue: "0",
      clearDisplay: false,
      operation: null,
      values: [0, 1],
      current: 0,
    };
  },

  components: { Button, Display },

  methods: {
    clearMemory() {
      Object.assign(this.$data, this.$options.data());
    },
    setOperation(operation) {
      if (this.current === 0) {
        this.operation = operation;
        this.current = 1;
        this.clearDisplay = true;
      } else {
        const equals = operation === "=";
        const currentOperation = this.operation;

        try {
          this.values[0] = eval(
            `${this.values[0]} ${currentOperation} ${this.values[1]}`
          );
          if (isNaN(this.values[0] || !isFinite(this.values[0]))) {
            this.clearMemory();
            return;
          }
        } catch (e) {
          this.$emit("onError", e);
        }

        this.values[1] = 0;
        this.displayValue = this.values[0];
        this.operation = equals ? null : operation; // se o operador for "=" termina a operação senao coloca a nova operação
        this.current = equals ? 0 : 1; // se digitou "=" continua mexedo no primeiro senao passa a mexer no segundo
        this.clearDisplay = !equals; // limpa o display apos o "=" (no proximo click)
      }
    },
    addDigit(n) {
      if (n === "." && this.displayValue.includes(".")) {
        return;
      }

      const clearDisplay = this.displayValue === "0" || this.clearDisplay;
      const currentValue = clearDisplay ? "" : this.displayValue;
      const value = currentValue + n;

      this.displayValue = value;
      this.clearDisplay = false;

      if (n !== ".") {
        const i = this.current;
        const newValue = parseFloat(value);
        this.values[i] = newValue;
      }
    },
  },
};
</script>

<style>
.calculator {
  border-radius: 5px;
  display: grid;
  grid-template-columns: repeat(4, 25%);
  grid-template-rows: 1fr 48px 48px 48px 48px 48px;
  height: 320px;
  overflow: hidden;
  width: 235px;
}
</style>