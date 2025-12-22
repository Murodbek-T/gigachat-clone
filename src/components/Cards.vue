<script setup>
import { onMounted, ref } from "vue";
import gsap from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";
gsap.registerPlugin(ScrollTrigger);
const cardsRef = ref(null);

defineProps({
  card: Object,
});

onMounted(() => {
  gsap.from(cardsRef.value, {
    scrollTrigger: {
      trigger: cardsRef.value,
      start: "top 80%",
      end: "top 20%",
      scrub: true,
    },
    opacity: 0,
  });
});
</script>

<template>
  <div class="card" ref="cardsRef">
    <img :src="card.imgUrl" :alt="card.title" class="card-image" />

    <div class="card-header">
      <div v-if="card.id === 4" class="badge">Создайте видео с образом</div>
      <button class="favorite-btn">
        <svg
          viewBox="0 0 24 24"
          width="20"
          height="20"
          fill="none"
          stroke="currentColor"
          stroke-width="2"
        >
          <path
            d="M12 2l3.09 6.26L22 9.27l-5 4.87 1.18 6.88L12 17.77l-6.18 3.25L7 14.14 2 9.27l6.91-1.01L12 2z"
          />
        </svg>
      </button>
    </div>

    <div class="card-footer">
      <h3 class="card-title">{{ card.title }}</h3>
      <p class="card-subtitle">{{ card.subtitle }}</p>
    </div>
  </div>
</template>

<style scoped>
.card {
  position: relative;
  width: 100%;
  aspect-ratio: 16 / 10;
  border-radius: 24px;
  overflow: hidden;
  background-color: #2a2a2a;
  margin-bottom: 16px;
  cursor: pointer;
}

.card-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.5s ease;
}

.card:hover .card-image {
  transform: scale(1.05);
}

/* Header: Badge and Star */
.card-header {
  position: absolute;
  top: 12px;
  left: 12px;
  right: 12px;
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
}

.badge {
  background: rgba(255, 255, 255, 0.2);
  backdrop-filter: blur(10px);
  -webkit-backdrop-filter: blur(10px);
  padding: 6px 12px;
  border-radius: 12px;
  font-size: 12px;
  font-weight: 600;
  color: white;
  border: 1px solid rgba(255, 255, 255, 0.3);
}

.favorite-btn {
  background: rgba(0, 0, 0, 0.4);
  backdrop-filter: blur(8px);
  border: none;
  width: 36px;
  height: 36px;
  border-radius: 10px;
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  transition: background 0.2s;
}

.favorite-btn:hover {
  background: rgba(0, 0, 0, 0.6);
}

/* Footer: Text with Gradient for readability */
.card-footer {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  padding: 40px 16px 16px;
  background: linear-gradient(to top, rgba(0, 0, 0, 0.8) 0%, transparent 100%);
  color: white;
  display: flex;
  flex-direction: column;
  gap: 4px;
}

.card-title {
  font-size: 18px;
  font-weight: 700;
  margin: 0;
}

.card-subtitle {
  font-size: 13px;
  opacity: 0.8;
  margin: 0;
  line-height: 1.4;
}
</style>
