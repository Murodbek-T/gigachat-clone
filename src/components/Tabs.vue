<script setup>
import { ref } from "vue";

// The state that controls which content is shown
const activeValue = ref("all");

const tabs = [
  { label: "Все", value: "all" },
  { label: "Избранные", value: "favorites" },
];
</script>

<template>
  <div class="tabs-root">
    <div class="tabs-list">
      <h1>Функции</h1>
      <div>
        <button
          v-for="tab in tabs"
          :key="tab.value"
          @click="activeValue = tab.value"
          :class="['tab-trigger', { active: activeValue === tab.value }]"
        >
          {{ tab.label }}
        </button>
      </div>
    </div>

    <div class="tab-viewport">
      <div v-if="activeValue === 'all'" class="tab-content">
        <div class="grid-layout">
          <slot name="all-content">
            <p>Rendering all functions...</p>
          </slot>
        </div>
      </div>

      <div v-else-if="activeValue === 'favorites'" class="tab-content">
        <div class="empty-state">
          <svg
            viewBox="0 0 24 24"
            width="35"
            height="35"
            fill="none"
            stroke="currentColor"
            stroke-width="2"
          >
            <path
              d="M12 2l3.09 6.26L22 9.27l-5 4.87 1.18 6.88L12 17.77l-6.18 3.25L7 14.14 2 9.27l6.91-1.01L12 2z"
            />
          </svg>
          <h1>Ваши любимые функции будут здесь</h1>
          <p>Добавляйте их с помощью звёздочки</p>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
/* Container for the tab buttons */
.tabs-list {
  display: flex;
  gap: 20px;
  flex-direction: column;
  width: 100%;
  margin-bottom: 24px;
  position: sticky;
  top: 0;
  padding: 10px 0px;
  z-index: 99999;
  background: var(--bg-color);
}

/* Individual pill buttons */
.tab-trigger {
  padding: 8px 24px;
  border-radius: 40px;
  font-size: 14px;
  font-weight: 600;
  cursor: pointer;
  border: none;
  background: var(--dock-bg);
  color: var(--text-color);
  transition: all 0.2s ease;
}

.tab-trigger:hover {
  background-color: var(--tab-hover-color);
}

/* Active state matching your screenshot */
.tab-trigger.active {
  background-color: var(--text-color);
  color: var(--bg-color);
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.2);
}

/* Content area */
.tab-content {
  animation: fadeIn 0.3s ease;
}

.empty-state {
  margin-top: 150px;
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
  gap: 5px;
}

.empty-state h1 {
  width: 80%;
  color: var(--text-color);
  font-size: var(--text-medium);
}
.empty-state p {
  color: var(--text-color);
  font-size: var(--text-small);
}

@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(4px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
</style>
