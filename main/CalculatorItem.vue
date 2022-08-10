<template>
  <div class="calculator">
    <display-item :value="displayValue" />
    <button-item label="AC" triple @calcClick="clearMemory" />
    <button-item label="/" operation @calcClick="setOperation" />
    <button-item label="7" @calcClick="addDigit" />
    <button-item label="8" @calcClick="addDigit" />
    <button-item label="9" @calcClick="addDigit" />
    <button-item label="*" operation @calcClick="setOperation" />
    <button-item label="4" @calcClick="addDigit" />
    <button-item label="5" @calcClick="addDigit" />
    <button-item label="6" @calcClick="addDigit" />
    <button-item label="-" operation @calcClick="setOperation" />
    <button-item label="1" @calcClick="addDigit" />
    <button-item label="2" @calcClick="addDigit" />
    <button-item label="3" @calcClick="addDigit" />
    <button-item label="+" operation @calcClick="setOperation" />
    <button-item label="0" double @calcClick="addDigit" />
    <button-item label="." @calcClick="addDigit" />
    <button-item label="=" operation @calcClick="setOperation" />
  </div>
</template>

<script>
import ButtonItem from "../components/ButtonItem.vue";
import DisplayItem from "../components/DisplayItem.vue";

export default {
  data: function () {
    return {
      displayValue: "0",
      clearDisplay: false,
      operation: null,
      values: [0, 0],
      current: 0,
    };
  },
  components: { ButtonItem, DisplayItem },
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
        } catch (e) {
          this.$emit("onError", e);
        }
        this.values[1] = 0;
        this.displayValue = this.values[0];
        this.operation = equals ? null : operation;
        this.current = equals ? 0 : 1;
        this.clearDisplay = !equals;
      }
    },
    addDigit(d) {
      if (d === "." && this.displayValue.includes(".")) {
        return;
      }

      const clearDisplay =
        (this.displayValue === "0" && d !== ".") || this.clearDisplay;
      const currentValue = clearDisplay ? "" : this.displayValue;
      const displayValue = currentValue + d;

      this.displayValue = displayValue;
      this.clearDisplay = false;

      if (d !== ".") {
        const i = this.current;
        const newValue = parseFloat(displayValue);
        this.values[i] = newValue;
      }
    },
  },
};
</script>

<style>
.calculator {
  height: 320px;
  width: 235px;
  border-radius: 5px;
  overflow: hidden;
  display: grid;
  grid-template-columns: repeat(4, 25%);
  grid-template-rows: 1fr 48px 48px 48px 48px 48px;
}
</style>