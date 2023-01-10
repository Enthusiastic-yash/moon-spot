<script setup>
import { ref } from "vue";

let points = ref([]);
let deletePoint = ref([]);

const domClick = (e) => {
  points.value.push({
    x: (e.offsetX / innerWidth) * 100,
    y: (e.offsetY / innerHeight) * 100,
  });
};

const undoPoint = () => {
  let undo = points.value.pop();
  deletePoint.value.push(undo);
};

const redoPoint = () => {
  let redo = deletePoint.value.pop();
  points.value.push(redo);
};
</script>

<template>
  <button @click="undoPoint">Undo</button>
  <button @click="redoPoint">Redo</button>
  <div class="Box" @click="domClick">
    <div
      v-for="point in points"
      class="dot"
      :style="{ top: `${point.y}%`, left: `${point.x}%` }"
    ></div>
  </div>
</template>

<style scoped>
.Box {
  height: 100vh;
  background-color: gray;
  position: relative;
}
.dot {
  width: 20px;
  border-radius: 50%;
  height: 20px;
  background-color: white;
  position: absolute;
}
</style>
