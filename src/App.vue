<template>
  <div class="wrapper">
    <h1>Vue 3 CRUD Application</h1>
    <UserCrud />
  </div>
</template>

<script setup>
import UserCrud from "./components/UserCrud.vue";
</script>

<style>
.wrapper {
  padding: 40px;
  font-family: Arial, sans-serif;
  text-align: center;
}
</style>
