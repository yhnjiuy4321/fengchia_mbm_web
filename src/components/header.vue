<script setup>
import { useRouter } from 'vue-router'
import Logo from '/logonNoBg1.png'

const router = useRouter()

const gohome = () => {
  router.push("/homepage")
}
</script>

<template>
  <header class="header">
    <div class="ocean">
      <div class="wave"></div>
      <div class="wave"></div>
    </div>
    <div class="header-content">
      <div class="logo-container" @click="gohome">
        <img :src="Logo" alt="Marine Museum Logo" class="logo">
      </div>
      <div class="site-name" @click="gohome">
        <h1 class="chinese-name">逢甲海洋生物博物館</h1>
        <span class="eng-name">Feng Chia Marine Biology Museum</span>
      </div>
    </div>
  </header>
</template>

<style scoped>
.header {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 80px;
  z-index: 1000;
  background: linear-gradient(to right, #1a4c7c, #2d82b5);
  overflow: hidden;
}

.header-content {
  display: flex;
  align-items: center;
  max-width: 1400px;
  margin: 0 auto;
  padding: 10px 24px;
  position: relative;
  z-index: 2;
}

.logo-container {
  cursor: pointer;
  margin-right: 20px;
  transition: transform 0.3s ease;
}

.logo-container:hover {
  transform: scale(1.1);
}

.logo {
  width: 80px;
  height: 80px;
  object-fit: contain;
  filter: drop-shadow(0 2px 4px rgba(0, 0, 0, 0.2));
}

.site-name {
  display: flex;
  flex-direction: column;
  cursor: pointer;
  transition: all 0.3s ease;
}

.chinese-name {
  margin: 0;
  font-size: 28px;
  font-weight: 600;
  color: #ffffff;
  text-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
}

.eng-name {
  font-size: 14px;
  color: #b3e0ff;
  letter-spacing: 1px;
}

/* 海浪動畫 */
.ocean {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  height: 40px;
  opacity: 0.3;
}

.wave {
  position: absolute;
  top: 0;
  left: 0;
  width: 200%;
  height: 100%;
  background: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 800 88.7'%3E%3Cpath d='M800 56.9c-155.5 0-204.9-50-405.5-49.9-200 0-250 49.9-394.5 49.9v31.8h800v-.2-31.6z' fill='%23ffffff'/%3E%3C/svg%3E");
  animation: wave 7s linear infinite;
  transform: translate3d(0, 0, 0);
}

.wave:nth-of-type(2) {
  top: 10px;
  animation: wave 9s linear infinite;
  opacity: 0.6;
}

@keyframes wave {
  0% { transform: translateX(0) }
  50% { transform: translateX(-25%) }
  100% { transform: translateX(-50%) }
}

/* 響應式設計 */
@media (max-width: 768px) {
  .header {
    height: 70px;
  }

  .header-content {
    padding: 8px 16px;
  }

  .logo {
    width: 40px;
    height: 40px;
  }

  .chinese-name {
    font-size: 24px;
  }

  .eng-name {
    font-size: 12px;
  }
}

@media (max-width: 480px) {
  .header {
    height: 60px;
  }

  .logo {
    width: 35px;
    height: 35px;
  }

  .chinese-name {
    font-size: 20px;
  }

  .eng-name {
    font-size: 10px;
  }
}
</style>