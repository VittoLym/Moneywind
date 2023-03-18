<template>
  <Layout>
    <template #Header>
      <Header></Header>
    </template>
    <template #Resume>
      <Resume
        :label="'ahorro total'"
        :totalAmount="totalAmount"
        :amount="amount"
      >
        <template #graphic>
          <Graphic :amounts="amounts" @select="select" />
        </template>
        <template #Action>
          <slot name="Action"> <Action @create="create" /> </slot>
        </template>
      </Resume>
    </template>
    <template #Movements>
      <Movements :movements="movements" @remove="remove" />
    </template>
  </Layout>
</template>
<script>
import Layout from "./MyLayout.vue";
import Header from "./MyHeader.vue";
import Resume from "./Resume/MyIndex.vue";
import Action from "./MyAction.vue";
import Movements from "./Movements/MyIndex.vue";
import Graphic from "./Resume/ElGraphic.vue";
export default {
  components: {
    Layout,
    Header,
    Resume,
    Movements,
    Action,
    Graphic,
  },
  data() {
    return {
      label: null,
      amount: null,
      movements: [],
    };
  },
  computed: {
    amounts() {
      const lastDays = this.movements.map((m) => m.amount);
      return lastDays.map((m, i) => {
        const lastMovements = lastDays.slice(0, i + 1);
        return lastMovements.reduce((suma, movement) => {
          const total = suma + movement;
          return total;
        }, 0);
      });
    },
    totalAmount() {
      return this.movements.reduce((suma, m) => {
        return suma + m.amount;
      }, 0);
    },
  },
  mounted() {
    const movements = JSON.parse(localStorage.getItem("movements"));
    if (Array.isArray(movements)) {
      this.movements = movements.map((m) => {
        return { ...m, time: new Date(m.time) };
      });
    }
  },
  methods: {
    save() {
      localStorage.setItem("movements", JSON.stringify(this.movements));
    },
    remove(id) {
      const index = this.movements.findIndex((m) => m.id === id);
      this.movements.splice(index, 1);
      this.save();
    },
    create(movement) {
      this.movements.push(movement);
      this.save();
    },
    select(el) {
      this.amount = el;
    },
  },
};
</script>
