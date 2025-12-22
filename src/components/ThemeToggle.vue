<script setup>
import { ref, onMounted } from "vue";

const isDark = ref(true);

const toggleTheme = () => {
  isDark.value = !isDark.value;
  // Apply the theme to the root element
  document.documentElement.setAttribute(
    "data-theme",
    isDark.value ? "dark" : "light"
  );
  // Optional: Save to localStorage
  localStorage.setItem("user-theme", isDark.value ? "dark" : "light");
};

onMounted(() => {
  const savedTheme = localStorage.getItem("user-theme") || "dark";
  isDark.value = savedTheme === "dark";
  document.documentElement.setAttribute("data-theme", savedTheme);
});

</script>

<template>
  <div class="toggle-wrapper" @click="toggleTheme">
    <span class="toggle-label">Тёмная тема</span>
    <div class="switch" :class="{ 'is-active': isDark }">
      <div class="handle"></div>
    </div>
  </div>
</template>

<style scoped>
.toggle-wrapper {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px 20px;
  cursor: pointer;
  border-radius: 100px; 
}

.toggle-label {
  font-size: 16px;
  font-weight: 600;
  color: var(--text-color);
}

.switch {
  width: 44px;
  height: 24px;
  background-color: var(--pill-bg); /* Using your existing var */
  border-radius: 20px;
  position: relative;
  transition: background-color 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  border: 1px solid black;
}

.switch.is-active {
  background-color: #00d38d;
}

.handle {
  width: 20px;
  height: 20px;
  background-color: var(--text-color);
  border-radius: 50%;
  position: absolute;
  top: 2px;
  left: 2px;
  transition: transform 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
}

.switch.is-active .handle {
  transform: translateX(20px);
}
</style>
