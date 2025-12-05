<template>
  <div id="app">
    <h1>Welcome to My Vue.js App on Azure!</h1>
    <p>{{ message }}</p>
    <p>API URL: {{ apiUrl }}</p>
    <button @click="changeMessage">Click Me</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      message: process.env.VUE_APP_TITLE,
      apiUrl: process.env.VUE_APP_API_URL
    };
  },
  methods: {
    changeMessage() {
      this.message = "You clicked the button!";
    }
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  margin-top: 40px;
}
button {
  padding: 10px 20px;
  margin-top: 20px;
  cursor: pointer;
}
</style>
