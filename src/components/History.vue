<template>
  <div class="history-container">
    <div class="empty-state2">
      <div class="chat-icon">
        <img src="../assets/icons/bubble.svg" alt="bubble" width="100" />
      </div>

      <h2 class="title">У вас ещё нет чатов</h2>

      <p class="description">Напишите GigaChat свой первый запрос.</p>

      <p class="hint">
        Если вы вышли из аккаунта, откройте «Профиль» и войдите по номеру
        телефона — так мы сможем вернуть вашу историю чатов
      </p>

      <button class="new-chat-btn">Новый чат</button>
    </div>
  </div>
</template>

<style scoped>
.history-container {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 70vh;
}

.empty-state2 {
  text-align: center;
  max-width: 340px;
}

.title {
  font-size: 24px;
  font-weight: 700;
  margin-bottom: 12px;
}

.description {
  font-size: 16px;
  margin-bottom: 8px;
}

.hint {
  font-size: 14px;
  color: var(--text-color);
  line-height: 1.4;
  margin-bottom: 32px;
}

.new-chat-btn {
  background: var(--text-color);
  color: var(--bg-color);
  border: none;
  padding: 14px 48px;
  border-radius: 100px;
  font-size: 16px;
  font-weight: 600;
  cursor: pointer;
}
</style>
