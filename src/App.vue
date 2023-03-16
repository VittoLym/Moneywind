<template>
  <Suspense>
    <template #default>
      <MyHome />
    </template>
    <template #fallback>
      <SplashScreen />
    </template>
  </Suspense>
</template>

<script>
import { defineAsyncComponent } from "vue";
import SplashScreen from "@/components/SplashScreen.vue";
export default {
  components: {
    SplashScreen,
    MyHome: defineAsyncComponent(
      () =>
        new Promise((resolve) => {
          setTimeout(() => {
            resolve(require("./components/MyHome.vue"));
          }, 2500);
        })
    ),
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  display: flex;
  flex-direction: column;
  color: #2c3e50;
  height: 90vh;
  justify-content: space-between;
}
#app .splasScreen {
  justify-content: left;
}
body {
  background-color: #181818;
  margin: 0;
}
div .Header header {
  display: flex;
  justify-content: space-between;
  margin: 1% 1% 0 1%;
}
</style>
