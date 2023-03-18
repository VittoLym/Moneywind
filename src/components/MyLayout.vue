<template>
  <div class="header">
    <slot name="Header"></slot>
  </div>
  <div class="resume">
    <slot name="Resume"></slot>
  </div>
  <div class="movements">
    <div class="head" @click="showMovements = !showMovements">
      <div class="grip"></div>
    </div>
    <div class="body" v-show="showMovements">
      <slot name="Movements"></slot>
    </div>
  </div>
</template>
<script setup>
import { ref } from "vue";

const showMovements = ref(false);
</script>
<style scoped>
.header,
.resume,
.movements {
  display: flex;
  justify-content: space-around;
  align-items: center;
  padding: 2% 0;
  box-sizing: border-box;
}
.header {
  position: fixed;
  width: 100vw;
}
.resume {
  min-height: 100vh;
}
.movements {
  z-index: 1;
  position: absolute;
  flex-direction: column;
  bottom: 0;
  width: 100vw;
  background-color: #181818;
  box-shadow: 0 -8px 16px #242424;
  border-radius: 24px;
  overflow: hidden;
}
.movements .head {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 24px;
  width: 100%;
  box-sizing: border-box;
}
.movements .body {
  height: 75vh;
  width: 100%;
}
.movements .head .grip {
  width: 120px;
  height: 8px;
  background-color: #333;
  border-radius: 4px;
}
@media (min-width: 890px) {
  .header,
  .resume,
  .movements {
    padding: 0;
  }
}
</style>
