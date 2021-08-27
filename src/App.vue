<template>
  <div class="cols">
    <textarea v-model="inputA" placeholder="language A" />
    <textarea v-model="inputB" placeholder="language B" />
    <textarea v-model="output" readonly />
  </div>
</template>

<script setup lang="ts">
import leven from "leven";
import { computed, ref } from "vue";

function zip<T>(a: T[], b: T[]) {
  return Array.from(Array(Math.max(b.length, a.length)), (_, i) => [
    a[i] ?? "",
    b[i] ?? "",
  ]);
}

const inputA = ref("");
const inputB = ref("");
const output = computed(() => {
  const pairs = zip(inputA.value.split("\n"), inputB.value.split("\n"));
  console.log("pairs", pairs);
  return pairs.reduce((sum, [a, b]) => sum + leven(a, b), 0) / pairs.length;
});
</script>

<style>
html,
body,
#app {
  height: 90%;

  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.cols,
.cols * {
  height: 512px;
}
</style>
