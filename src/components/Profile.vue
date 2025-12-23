<script setup>
import { ref } from "vue";
import ThemeToggle from "./ThemeToggle.vue";
// Component Icons
import Web from "./icons/Web.vue";
import Vk from "./icons/Vk.vue";
import SettingsIcon from "./icons/SettingsIcon.vue";
import QuestionIcon from "./icons/QuestionIcon.vue";
import BotIcon from "./icons/BotIcon.vue";
import FeedbackIcon from "./icons/FeedbackIcon.vue";
import ChevronRightIcon from "./icons/ChevronRightIcon.vue";
// State to manage which 'window' is visible
const currentView = ref("main"); // options: 'main', 'settings', 'about', etc.

const menuItems = [
  {
    id: "settings",
    title: "Настройки",
    icon: SettingsIcon,
  },
  {
    id: "about",
    title: "Про GigaChat",
    icon: BotIcon,
  },
  {
    id: "feedback",
    title: "Поделиться мнением",
    icon: FeedbackIcon,
  },
  {
    id: "support",
    title: "Написать в поддержку",
    icon: QuestionIcon,
  },
];
</script>

<template>
  <div class="profile-container">
    <div v-if="currentView === 'main'" class="view-fade">
      <p class="promo-header">
        Объедините все чаты из Telegram, веб-версии и приложения GigaChat
      </p>

      <button class="login-button">Войти по номеру телефона</button>

      <div class="menu-section">
        <div
          v-for="item in menuItems"
          :key="item.id"
          class="menu-row"
          @click="currentView = item.id"
        >
          <div class="row-left">
            <component :is="item.icon" class="row-icon" />
            <span class="row-title">{{ item.title }}</span>
          </div>

          <ChevronRightIcon />
        </div>
      </div>
      <div class="separator"></div>

      <div class="menu-section">
        <div class="menu-row">
          <span class="row-title">
            <Web />
            GigaChat в веб-версии</span
          >
          <ChevronRightIcon />
        </div>
        <div class="menu-row">
          <span class="row-title">
            <Vk />
            GigaChat в VK</span
          >
          <ChevronRightIcon />
        </div>
      </div>

      <p class="legal-link">Пользовательское соглашение</p>
    </div>

    <div v-else-if="currentView === 'settings'" class="view-slide">
      <div class="view-header">
        <button class="back-btn" @click="currentView = 'main'">
          <img src="../assets/icons/chevron-left.svg" alt="left" width="25" />
        </button>
      </div>

      <div class="settings-content">
        <p class="empty-note"><ThemeToggle /></p>
      </div>
    </div>

    <div v-else class="view-slide">
      <div class="view-header">
        <button class="back-btn" @click="currentView = 'main'">
          <img src="../assets/icons/chevron-left.svg" alt="left" width="25" />
        </button>
      </div>
      <p class="empty-note">Этот раздел находится в разработке.</p>
    </div>
  </div>
</template>

<style scoped>
.profile-container {
  margin-top: 20px;
  color: var(--text-color);
}

.promo-header {
  font-size: 14px;
  color: var(--text-color);
  line-height: 1.4;
  margin-bottom: 16px;
}

.login-button {
  width: 100%;
  padding: 16px;
  background-color: #00d38d;
  color: var(--bg-color);
  border: none;
  border-radius: 16px;
  font-size: 16px;
  font-weight: 700;
  margin-bottom: 32px;
  cursor: pointer;
}

.menu-section {
  margin-bottom: 10px;
}

.menu-row {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px 12px;
  margin-bottom: 5px;
  cursor: pointer;
  border-radius: 50px;
}

.menu-row:hover {
  background: var(--menu-hover-color);
}

.row-left {
  display: flex;
  align-items: center;
  gap: 12px;
}

.row-icon {
  font-size: 20px;
  width: 20px;
  text-align: center;
}

.row-title {
  display: flex;
  align-items: center;
  gap: 10px;
  font-size: 16px;
  font-weight: 500;
}

.chevron {
  font-size: 24px;
  color: var(--text-color);
  font-weight: 300;
}

.legal-link {
  font-size: 14px;
  font-weight: 600;
  margin-top: 20px;
  cursor: pointer;
  color: #00d38d;
}

/* Sub-view Styles */
.view-header {
  display: flex;
  align-items: center;
  gap: 16px;
}

.back-btn {
  background: none;
  border: none;
  color: #00d38d;
  font-size: 16px;
  cursor: pointer;
  padding: 0;
}

.view-title {
  font-size: 20px;
  font-weight: 700;
}

.empty-note {
  color: var(--text-muted);
  text-align: center;
  margin-top: 40px;
}

.separator {
  background: var(--dock-bg);
  width: 100%;
  height: 1px;
  margin: 10px 0px;
}

/* Animations */
.view-fade {
  animation: fadeIn 0.3s ease-out;
}

.view-slide {
  animation: slideIn 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}

@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

@keyframes slideIn {
  from {
    transform: translateX(30px);
    opacity: 0;
  }
  to {
    transform: translateX(0);
    opacity: 1;
  }
}
</style>
