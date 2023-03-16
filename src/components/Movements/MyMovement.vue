<template>
  <div class="movement">
    <div class="content">
      <h4>{{ title }}</h4>
      <p>{{ description }}</p>
    </div>
    <div class="action">
      <img src="@/assets/trash-icon.svg" alt="borrar" @click="remove" />
      <p :class="{ red: isNegative, green: !isNegative }">{{ amountRef }}</p>
    </div>
  </div>
</template>
<script setup>
import { defineProps, toRefs, computed, defineEmits } from "vue";
const currencyFormatter = new Intl.NumberFormat("es-AR", {
  style: "currency",
  currency: "ARS",
});
const props = defineProps({
  title: {
    type: String,
  },
  id: {
    type: Date,
  },
  amount: {
    type: Number,
  },
  description: {
    type: String,
  },
});
const emit = defineEmits(["remove"]);
const { id, title, amount, description } = toRefs(props);
const remove = () => {
  emit("remove", id.value);
};
const isNegative = computed(() => amount.value < 0);
const amountRef = computed(() => currencyFormatter.format(amount.value));
</script>
<style scoped>
.movement {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  padding: 16px;
  background-color: #181818;
  border-radius: 8px;
  box-sizing: border-box;
  color: aquamarine;
}
.movement .content {
  width: 100%;
  text-align: start;
}
.movement .action {
  display: flex;
  justify-content: space-between;
  align-items: flex-end;
  flex-direction: column;
}
h4,
p {
  margin: 0;
  padding: 0;
}
h4 {
  margin-bottom: 8px;
}
.movement .action img {
  margin-bottom: 16px;
}
.red {
  color: red;
}
.green {
  color: green;
}
</style>
