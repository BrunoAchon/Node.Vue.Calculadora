<template>
  <div class="calculator">
    <Display />
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
  components: { Button, Display },
  methods: {
    clearMemory() {

    },
    setOperation(operation) {
      console.log(operation);
    },
    addDigit(n) {
      console.log(n);
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