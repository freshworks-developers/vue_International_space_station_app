<template>
  <div id="app" class="App">
    <img src="../assets/vuejs.svg" class="vue_logo" alt="logo" />
    <img src="../assets/icon.svg" class="App-logo" alt="logo" />
    <h3>Hi {{agentName}}</h3>
    <p>Welcome to your first Vue app in Freshdesk</p>
  </div>
</template>

<script>
export default {
  name: "Sidebar",
  props: {
    agentName: String,
  }
};
</script>

<style scoped>
.vue_logo {
  height: 40vmin;
  color: red;
}
</style>