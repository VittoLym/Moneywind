<template>
  <div class="modal">
    <main class="head">
      <p>Nuevo Movimiento</p>
      <img @click="close" src="@/assets/equis-icon.png" alt="Cerrar" />
    </main>
    <article class="body">
      <slot></slot>
    </article>
  </div>
</template>
<script setup>
import { defineEmits } from "vue";
const emit = defineEmits(["close"]);
const close = () => emit("close");
</script>
<style scoped>
.modal {
  z-index: 2;
  position: absolute;
  left: 0;
  right: 0;
  top: 0;
  bottom: 0;
  background-color: #181818;
  color: #2c3e50;
}
.head {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  padding: 3% 3% 7% 0;
  box-sizing: border-box;
}
p {
  margin: 0;
  font-size: 1.5rem;
  color: #323232;
  margin-left: 5%;
}
.body {
  height: 80%;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
}
</style>
