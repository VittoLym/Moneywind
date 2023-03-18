<template>
  <svg
    @click="Click"
    @mousemove="Clicky"
    @mouseleave="unTap"
    @mouseup="unTap"
    @touchstart.passive="tap"
    @touchmove.passive="tap"
    @touchend="unTap"
    view-box="0 0 300 200"
  >
    <polyline fill="none" stroke="#36f" stroke-width="2" :points="points" />
    <line
      stroke="#639"
      stroke-width="3"
      x1="0"
      :y1="zero"
      x2="300"
      :y2="zero"
    />
    <line
      v-show="showPointer"
      stroke-width="2"
      stroke="#000"
      :x1="pointer"
      y1="0"
      :x2="pointer"
      y2="200"
    />
  </svg>
</template>
<script setup>
import { toRefs, defineProps, defineEmits, computed, ref, watch } from "vue";
const props = defineProps({
  amounts: {
    type: Array,
    default: () => [],
  },
});
const { amounts } = toRefs(props);
const amountToPixel = (amount) => {
  const min = Math.min(...amounts.value);
  const max = Math.max(...amounts.value);
  const amountAbs = amount + Math.abs(min);
  const minMax = Math.abs(max) + Math.abs(min);
  return 200 - ((amountAbs * 100) / minMax) * 2;
};
const zero = computed(() => {
  return amountToPixel(0);
});
const points = computed(() => {
  const total = amounts.value.length;
  return amounts.value.reduce((points, amount, i) => {
    const x = (300 / total) * (i + 1);
    const y = amountToPixel(amount);
    return `${points} ${x}, ${y}`;
  }, `0,${amountToPixel(amounts.value.length ? amounts.value[0] : 0)}`);
});
const showPointer = ref(false);
const pointer = ref(0);
watch(pointer, (Value) => {
  const index = Math.ceil(Value / (300 / amounts.value.length));
  if (index < 0 || index > amounts.value.length) return;
  emit("select", amounts.value[index - 1]);
});
const emit = defineEmits(["select"]);
const show = ref(false);
const Click = (click) => {
  const target = click.target;
  const elementRect = target.getBoundingClientRect();
  const elementX = elementRect.x;
  const elementWidth = elementRect.width;
  if (elementWidth <= 0 || isNaN(elementWidth)) {
    return;
  }
  const clientX = click.clientX;
  showPointer.value = true;
  pointer.value = ((clientX - elementX) * 300) / elementWidth;
  show.value = true;
};
const Clicky = () => {
  if (show.value) {
    showPointer.value = true;
  } else if (show.value == false) {
    showPointer.value = false;
  }
};
const tap = ({ target, touches }) => {
  const elementRect = target.getBoundingClientRect();
  const elementX = elementRect.x;
  const elementWidth = elementRect.width;
  const { clientX } = touches[0];
  showPointer.value = true;
  pointer.value = ((clientX - elementX) * 300) / elementWidth;
};
const unTap = () => {
  showPointer.value = false;
};
</script>
<style scoped>
line {
  z-index: 400;
}
svg {
  min-height: 200px;
  background-color: #181818;
}
p {
  text-align: center;
}
</style>
