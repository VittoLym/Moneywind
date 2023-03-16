<template>
  <div>
    <main class="splashScreen">
      <img src="@/assets/logo.png" alt="Company logo" />
    </main>
    <h1><span>Money</span>Wind</h1>
  </div>
</template>
<style scoped>
.splashScreen {
  display: flex;
  justify-content: space-between;
  flex-direction: column;
  height: 40vh;
  margin: 40% 20% 0 20%;
}
h1 {
  color: #629;
  margin: 0;
  margin-bottom: 20vh;
}
h1 span {
  color: #242424;
}
img {
  margin: 0 10%;
  height: 50vh;
  margin: 0 20%;
  justify-content: center;
}
</style>
