<script setup>
import { onBeforeMount } from "vue";
import Dock from "./components/Dock.vue";

onBeforeMount(() => {
  const savedTheme = localStorage.getItem("user-theme") || "dark";
  document.documentElement.setAttribute("data-theme", savedTheme);
});
</script>

<template>
  <div class="main-container">
    <Dock />
  </div>
</template>

<style scoped>
.main-container {
  padding: 15px;
  border-radius: 30px !important;
 
}
</style>
