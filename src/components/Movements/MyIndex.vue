<template>
  <div class="Movements" :key="movements">
    <h2 class="title">Historial</h2>
    <div class="content" v-if="movements.length">
      <movement
        v-for="{ id, title, amount, description } in movements"
        :key="id"
        :id="new Date(id)"
        :title="title"
        :amount="amount"
        :description="description"
        @remove="handleRemove(id)"
      />
    </div>
    <p v-else>No hay movimientos</p>
  </div>
</template>

<script setup>
import { toRefs, defineProps, defineEmits } from "vue";
import movement from "./MyMovement.vue";

const props = defineProps({
  movements: {
    type: Array,
    default: () => [],
  },
});

const emit = defineEmits(["remove"]);

const handleRemove = (id) => {
  emit("remove", id);
};

const { movements } = toRefs(props);
</script>
<style scoped>
.title {
  margin: 8px 16px 24px 16px;
  color: var(--brand-blue);
}
.content {
  max-height: 68vh;
  display: flex;
  flex-direction: column;
  gap: 8px;
  overflow-x: hidden;
  color: aquamarine;
}
.content::-webkit-scrollbar {
  width: 2%;
}
.content::-webkit-scrollbar-thumb {
  background-color: #629;
  border-radius: 4%;
}
.content p {
  max-width: 75%;
  word-wrap: break-word;
  overflow-wrap: break-word;
}
</style>
