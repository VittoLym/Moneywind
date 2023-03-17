<template>
  <main>
    <p>{{ label }}</p>
    <h1>{{ amountCurrency }}</h1>
    <div class="graphic">
      <slot name="graphic"></slot>
    </div>
    <div class="action">
      <slot name="Action"></slot>
    </div>
  </main>
</template>
<script>
const currencyFormatter = new Intl.NumberFormat("es-AR", {
  style: "currency",
  currency: "ARS",
});
export default {
  props: {
    label: {
      type: String,
    },
    totalAmount: {
      type: Number,
    },
    amount: {
      type: Number,
      default: null,
    },
  },
  computed: {
    visualAmount() {
      return this.amount !== null ? this.amount : this.totalAmount;
    },
    amountCurrency() {
      return currencyFormatter.format(this.visualAmount);
    },
  },
};
</script>
<style scoped>
main {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  width: 100%;
}
h1,
p {
  margin: 0;
  text-align: center;
}
h1 {
  margin-top: 1.5%;
}
.graphic {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100vw;
  padding: 48px 2%;
  box-sizing: border-box;
  flex-direction: column;
}
@media (min-width: 900px) {
  p {
    margin: 0;
  }
  h1 {
    margin: 0;
  }
  .graphic {
    padding-top: 3%;
    padding-bottom: 0;
  }
  main {
    height: 100vh;
  }
}
</style>
