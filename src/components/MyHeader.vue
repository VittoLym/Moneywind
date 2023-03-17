<template>
  <header>
    <img @click="reload" src="@/assets/favicon.png" alt="Company Logo" />
    <h1><span>Money</span>Wind</h1>
    <span></span>
  </header>
</template>
<script>
export default {
  methods: {
    reload() {
      location.reload();
    },
  },
};
</script>
<style scoped>
header {
  margin-top: 2%;
  display: flex;
  justify-content: space-around;
  align-items: center;
  width: 98vw;
}
img,
span {
  width: 18%;
}

h1 {
  color: #629;
  height: 17px;
  margin: 0;
}

h1 span {
  color: #242424;
}

/* Estilos para pantallas medianas y grandes */
@media (min-width: 688px) {
  header {
    margin-top: 20px;
    margin-bottom: 20px;
  }

  img,
  span {
    width: 13%;
  }
  h1 {
    font-size: 3.6rem;
  }
  @media (min-width: 890px) {
    header {
      margin: 0;
      padding: 0;
    }
  }
}
</style>
