<script setup>
import { onMounted, ref } from "vue";
import PillTabs from "./Tabs.vue";
import Cards from "./Cards.vue";
import { cardsContent } from "../data/data";
import gsap from "gsap";
import History from "./History.vue";
import Profile from "./Profile.vue"

const activeTab = ref(1);

const dockButtons = [
  {
    id: 1,
    title: "Главная",
    icon: new URL("../assets/icons/home.svg", import.meta.url).href,
  },
  {
    id: 2,
    title: "История",
    icon: new URL("../assets/icons/history.svg", import.meta.url).href,
  },
  {
    id: 3,
    title: "Профиль",
    icon: new URL("../assets/icons/user.svg", import.meta.url).href,
  },
];

onMounted(() => {
  gsap.from(".dock-glass", {
    y: 100,
    opacity: 0,
    delay: 0.2,
    duration: 0.3,
  });
});
</script>

<template>
  <div class="app-wrapper">
    <div class="tab-viewport">
      <div v-if="activeTab === 1">
        <h1>Функции</h1>
        <PillTabs class="tabs">
          <template #all-content>
            <div class="card-grid">
              <Cards v-for="item in cardsContent" :key="item.id" :card="item" />
            </div>
          </template>
        </PillTabs>
      </div>
      <div v-if="activeTab === 2"><h1>История</h1>
      <History />
      </div>
      <div v-if="activeTab === 3"><h1>Профиль</h1>
      <Profile />
      </div>
    </div>

    <nav class="dock-container">
      <div class="dock-glass">
        <div
          v-for="item in dockButtons"
          :key="item.id"
          class="dock-item"
          @click="activeTab = item.id"
        >
          <div
            class="icon-circle"
            :class="{ 'is-active': activeTab === item.id }"
          >
            <img :src="item.icon" class="dock-icon" />
          </div>
          <span
            class="dock-label"
            :class="{ 'label-active': activeTab === item.id }"
          >
            {{ item.title }}
          </span>
        </div>
      </div>
    </nav>
  </div>
</template>

<style scoped>
.app-wrapper {
  padding: 20px;
  min-height: 100vh;
}

.dock-container {
  position: fixed;
  bottom: 50px;
  left: 50%;
  transform: translateX(-50%);
  z-index: 1000;
}

.dock-glass {
  display: flex;
  align-items: center;
  gap: 12px;
  padding: 2px;
  background: var(--dock-bg);
  backdrop-filter: blur(12px);
  -webkit-backdrop-filter: blur(12px);
  border: 1px solid var(--dock-border);
  border-radius: 50px;
}

.dock-item {
  display: flex;
  flex-direction: column;
  align-items: center;
  cursor: pointer;
  width: 60px;
}

.icon-circle {
  width: 48px;
  height: 48px;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 50%;
  transition: background 0.3s ease;
}

.icon-circle.is-active {
  background: var(--dock-active-circle);
  border: 2px solid black;
}


.dock-icon {
  width: 24px;
  height: 24px;
  filter: var(--icon-filter);
  transition: filter 0.3s ease;
}

.dock-label {
  position: absolute;
  bottom: -25px;
  font-size: 12px;
  font-weight: 600;
  color: var(--text-color);
  opacity: 0.6;
}

.label-active {
  opacity: 1;
}

.tabs {
  margin-top: 20px;
}
</style>
