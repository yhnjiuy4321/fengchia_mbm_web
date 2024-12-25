<script setup>
import { useRouter } from 'vue-router'
import { menu } from "@/data/homepage/menu.js"

const router = useRouter()
const menuList = menu

const navigationMethods = {
  goToQA: () => router.push('/homepage/Q&A'),
  goToShow: () => router.push('/homepage/Show'),
  goToNews: () => router.push('/homepage/News'),
  goToVenueTour: () => router.push('/homepage/VenueTour'),
  goToTicket: () => router.push('/homepage/ticketShop'),
  goToBio: () => router.push('/homepage/bioIdentiy')
}
</script>

<template>
  <div class="menu-container">
    <div class="wave-background">
      <div class="wave"></div>
      <div class="wave"></div>
    </div>

    <div class="content-wrapper">
      <h1 class="section-title">功能列表</h1>

      <div class="menu-grid">
        <template v-for="menuItem in menuList" :key="menuItem.id">
          <!-- 場館導覽 -->
          <div class="menu-card">
            <h5 class="card-title">{{ menuItem.name1 }}</h5>
            <div class="card-cover" @click="navigationMethods.goToVenueTour">
              <img :src="menuItem.photo1" alt="場館導覽">
              <div class="hover-content">
                <span class="icon">🏛️</span>
                <span class="text">點擊進入</span>
              </div>
            </div>
          </div>

          <!-- 服務與售票 -->
          <div class="menu-card">
            <h5 class="card-title">{{ menuItem.name2 }}</h5>
            <div class="card-cover" @click="navigationMethods.goToTicket">
              <img :src="menuItem.photo2" alt="服務與售票">
              <div class="hover-content">
                <span class="icon">🎟️</span>
                <span class="text">點擊進入</span>
              </div>
            </div>
          </div>

          <!-- 表演活動 -->
          <div class="menu-card">
            <h5 class="card-title">{{ menuItem.name3 }}</h5>
            <div class="card-cover" @click="navigationMethods.goToShow">
              <img :src="menuItem.photo3" alt="表演活動">
              <div class="hover-content">
                <span class="icon">🎭</span>
                <span class="text">點擊進入</span>
              </div>
            </div>
          </div>

          <!-- Q&A問答 -->
          <div class="menu-card">
            <h5 class="card-title">{{ menuItem.name4 }}</h5>
            <div class="card-cover" @click="navigationMethods.goToQA">
              <img :src="menuItem.photo4" alt="Q&A問答">
              <div class="hover-content">
                <span class="icon">❓</span>
                <span class="text">點擊進入</span>
              </div>
            </div>
          </div>

          <!-- 最新消息 -->
          <div class="menu-card">
            <h5 class="card-title">{{ menuItem.name5 }}</h5>
            <div class="card-cover" @click="navigationMethods.goToNews">
              <img :src="menuItem.photo5" alt="最新消息">
              <div class="hover-content">
                <span class="icon">📰</span>
                <span class="text">點擊進入</span>
              </div>
            </div>
          </div>

          <!-- 互動專區 -->
          <div class="menu-card">
            <h5 class="card-title">{{ menuItem.name6 }}</h5>
            <div class="card-cover" @click="navigationMethods.goToBio">
              <img :src="menuItem.photo6" alt="互動專區">
              <div class="hover-content">
                <span class="icon">🎮</span>
                <span class="text">點擊進入</span>
              </div>
            </div>
          </div>
        </template>
      </div>
    </div>
  </div>
</template>

<style scoped>
.menu-container {
  background: linear-gradient(135deg, #006994 0%, #003a61 100%);
  position: relative;
  overflow: hidden;
  padding: 40px 20px;
}

.wave-background {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  opacity: 0.1;
}

.wave {
  position: absolute;
  width: 200%;
  height: 200%;
  background: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 800 88.7'%3E%3Cpath d='M800 56.9c-155.5 0-204.9-50-405.5-49.9-200 0-250 49.9-394.5 49.9v31.8h800v-.2-31.6z' fill='%23ffffff'/%3E%3C/svg%3E");
  animation: wave 20s linear infinite;
}

.wave:nth-child(2) {
  top: 20%;
  animation: wave 15s linear infinite;
  opacity: 0.5;
}

@keyframes wave {
  0% { transform: translateX(0) translateZ(0) scaleY(1); }
  50% { transform: translateX(-25%) translateZ(0) scaleY(0.8); }
  100% { transform: translateX(-50%) translateZ(0) scaleY(1); }
}

.content-wrapper {
  position: relative;
  z-index: 1;
  max-width: 1600px;
  margin: 0 auto;
  padding: 20px 0;
}

.section-title {
  text-align: center;
  font-size: 2.5rem;
  color: #fff;
  margin-bottom: 2rem;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
  font-weight: 600;
}

.menu-grid {
  display: flex;
  justify-content: center;
  align-items: stretch;
  gap: 1rem;
  padding: 1rem;
  margin: 0 auto;
}

.menu-card {
  flex: 0 0 calc(16.666% - 1rem); /* 六個卡片平均分配空間 */
  min-width: 160px;
  max-width: 200px;
  background: rgba(255, 255, 255, 0.1);
  border-radius: 15px;
  overflow: hidden;
  box-shadow: 0 8px 32px rgba(31, 38, 135, 0.15);
  backdrop-filter: blur(4px);
  transition: transform 0.3s ease;
  display: flex;
  flex-direction: column;
}


.menu-card:hover {
  transform: translateY(-10px);
}

.card-title {
  color: #fff;
  text-align: center;
  padding: 0.75rem;
  margin: 0;
  font-size: 1rem;
  font-weight: 600;
  background: rgba(0, 0, 0, 0.2);
}

.card-cover {
  position: relative;
  aspect-ratio: 3/4; /* 更長的長寬比 */
  overflow: hidden;
  cursor: pointer;
  flex-grow: 1;
}

.card-cover img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.5s ease;
}

.hover-content {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 40, 85, 0.8);
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  opacity: 0;
  transition: opacity 0.3s ease;
}

.card-cover:hover .hover-content {
  opacity: 1;
}

.card-cover:hover img {
  transform: scale(1.1);
}

.icon {
  font-size: 2rem;
  margin-bottom: 0.75rem;
}

.text {
  color: #fff;
  font-size: 1rem;
  font-weight: 600;
}

/* 響應式設計 */
@media (max-width: 1200px) {
  .menu-card {
    flex: 0 0 calc(16.666% - 0.8rem);
    min-width: 140px;
  }
  .card-title {
    font-size: 0.9rem;
  }
}

@media (max-width: 992px) {
  .menu-grid {
    gap: 0.8rem;
    flex-wrap: wrap;
  }
  .menu-card {
    min-width: 120px;
  }
  .icon {
    font-size: 1.5rem;
  }
  .text {
    font-size: 0.9rem;
  }
}

@media (max-width: 768px) {
  .menu-card {
    min-width: 100px;
  }
  .card-title {
    padding: 0.5rem;
    font-size: 0.8rem;
  }
}

@media (max-width: 480px) {
  .menu-grid {
    grid-template-columns: 1fr;
  }

  .section-title {
    font-size: 1.8rem;
  }
}
</style>