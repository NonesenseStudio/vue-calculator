<template>
  <div>
    <div class="number">{{ inputs || 0 }}</div>
    <div class="equals">{{ result }}</div>
    <div class="keyboard">
      <el-button
        v-for="(item, index) in nums"
        :key="index"
        @click="onCalc(item)"
      >
        {{ item }}
      </el-button>
      <el-button
        v-for="(item, index) in keys"
        :key="index"
        @click="onCalc(item)"
      >
        {{ item }}
      </el-button>
      <el-button @click="clearEntry">CE</el-button>
    </div>
  </div>
</template>

<script lang="ts" setup>
import { ref, watch } from "vue";
let inputs = ref("");
let result = ref(0);
let isRepeat = /\W{2,}$/g;
let isZero = /\/0/g;
let nums = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];
let keys = [".", "+", "-", "=", "×", "÷"];
let error = false;
let onCalc = (selection: any) => {
  inputs.value += selection;
};
let clearEntry = () => {
  inputs.value = "";
  result.value = 0;
};
let t = ref("");

watch(inputs, (newValue, oldValue) => {
  if (isRepeat.test(inputs.value)) {
    inputs.value = inputs.value.replace(/(\W)(\1)+/g, "$2");
  }
  if (isZero.test(inputs.value)) {
    error = true;
  } else {
    error = false;
  }
  let num = inputs.value.match(/(?<=^|[\D]+)\-*\d+(?:\.?\d+|\d*)?/g);
  let symbol = inputs.value.match(/[^\w.=]/g);
  let equal = inputs.value.match(/=$/g);
  console.log(num);

  if (num && symbol) {
    result.value = Number(num[0]);
    for (let i = 1; i < num.length; i++) {
      result.value = floatOperate(result.value, num[i], symbol[i - 1]);
    }
  } else {
    result.value = 0;
  }
});

function floatOperate(arg1: any, arg2: any, symbol: any) {
  let result = 0;
  if (symbol === "+") {
    let r1, r2, m;
    try {
      r1 = arg1.toString().split(".")[1].length;
    } catch (e) {
      r1 = 0;
    }
    try {
      r2 = arg2.toString().split(".")[1].length;
    } catch (e) {
      r2 = 0;
    }
    m = Math.pow(10, Math.max(r1, r2));
    result = (arg1 * m + arg2 * m) / m;
  } else if (symbol === "-") {
    let r1, r2, m, n;
    try {
      r1 = arg1.toString().split(".")[1].length;
    } catch (e) {
      r1 = 0;
    }
    try {
      r2 = arg2.toString().split(".")[1].length;
    } catch (e) {
      r2 = 0;
    }
    m = Math.pow(10, Math.max(r1, r2));
    n = r1 >= r2 ? r1 : r2;
    result = Number(((arg1 * m - arg2 * m) / m).toFixed(n));
  } else if (symbol === "×") {
    let m = 0,
      s1 = arg1.toString(),
      s2 = arg2.toString();
    try {
      m += s1.split(".")[1].length;
    } catch (e) {}
    try {
      m += s2.split(".")[1].length;
    } catch (e) {}
    result =
      (Number(s1.replace(".", "")) * Number(s2.replace(".", ""))) /
      Math.pow(10, m);
  } else {
    let t1 = 0,
      t2 = 0,
      r1,
      r2;
    try {
      t1 = arg1.toString().split(".")[1].length;
    } catch (e) {}
    try {
      t2 = arg2.toString().split(".")[1].length;
    } catch (e) {}

    r1 = Number(arg1.toString().replace(".", ""));

    r2 = Number(arg2.toString().replace(".", ""));
    result = (r1 / r2) * Math.pow(10, t2 - t1);
  }

  console.log(arg1, arg2);

  return result;
}
</script>

<style></style>
