<script setup>
import pagehead from '@/components/header.vue'
import pagefooter from '@/components/footer.vue'
import carouselComponent from '@/components/carousel.vue'
import menuComponent from '@/components/NavMenu.vue'
import { aboutusContent } from "@/data/aboutusContent.js";
import {ref} from "vue";
const aboutus = ref(aboutusContent);
</script>

<template>
  <pagehead/>
  <carouselComponent/>
  <div class="d-flex mt-5">
    <menuComponent/>
    <div v-for="item in aboutus" :key="item.id" class="about-container">
      <!-- 標題區域 -->
      <div class="page-header">
        <div class="wave-animation"></div>
        <h1 class="main-title">{{ item.title }}</h1>
      </div>

      <!-- 內容區域 -->
      <div class="content-section">
        <!-- 第一段內容 -->
        <div class="content-block">
          <div class="text-content">
            <p>{{ item.content1 }}</p>
          </div>
          <div class="image-wrapper">
            <img src="@/assets/photo/about/about1.webp" alt="About Us" class="feature-image">
          </div>
        </div>

        <!-- 第二段內容 -->
        <div class="content-block reverse">
          <div class="text-content">
            <p>{{ item.content2 }}</p>
          </div>
          <div class="image-wrapper">
            <img src="@/assets/photo/about/open.webp" alt="Our Opening" class="feature-image">
          </div>
        </div>

        <!-- 第三段內容 -->
        <div class="content-block">
          <div class="text-content">
            <p>{{ item.content3 }}</p>
          </div>
          <div class="image-wrapper">
            <img src="@/assets/photo/about/about2.jpg" alt="Our Facilities" class="feature-image">
          </div>
        </div>
      </div>
    </div>
  </div>
  <pagefooter/>
</template>

<style scoped>
.about-container {
  width: 100%;
  padding: 2rem 4rem;
  background-color: #f8fcff;
}

/* 頁面標題樣式 */
.page-header {
  position: relative;
  background: linear-gradient(135deg, #006994 0%, #0099cc 100%);
  padding: 3rem;
  height: 140px;
  border-radius: 20px;
  text-align: center;
  overflow: hidden;
  margin-bottom: 3rem;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
}

.main-title {
  color: white;
  font-size: 3rem;
  font-weight: 700;
  margin: 0;
  position: relative;
  z-index: 1;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.2);
}

.wave-animation {
  position: absolute;
  bottom: 0;
  left: 0;
  width: 100%;
  height: 50px;
  background: url('data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAxNDQwIDMyMCI+PHBhdGggZmlsbD0icmdiYSgyNTUsMjU1LDI1NSwwLjEpIiBkPSJNMCwyMjR2OTZoMTQ0MHYtOTZjLTI4OSwwLTU3Ni0zMi04NjQtMzJTMjg5LDIyNCwwLDIyNHoiLz48L3N2Zz4=') repeat-x;
  animation: wave 20s linear infinite;
}

/* 內容區塊樣式 */
.content-section {
  max-width: 1200px;
  margin: 0 auto;
}

.content-block {
  display: flex;
  align-items: center;
  gap: 4rem;
  margin-bottom: 4rem;
  background: white;
  padding: 2rem;
  border-radius: 20px;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.05);
  transition: transform 0.3s ease;
}

.content-block:hover {
  transform: translateY(-5px);
}

.content-block.reverse {
  flex-direction: row-reverse;
}

.text-content {
  flex: 1;
  padding: 2rem;
}

.text-content p {
  color: #2c3e50;
  line-height: 1.8;
  font-size: 1.1rem;
  margin: 0;
  text-align: justify;
}

.image-wrapper {
  flex: 1;
  padding: 1rem;
}

.feature-image {
  width: 100%;
  height: auto;
  border-radius: 15px;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s ease;
  object-fit: cover;
}

.feature-image:hover {
  transform: scale(1.02);
}

/* 動畫效果 */
@keyframes wave {
  0% {
    background-position: 0 0;
  }
  100% {
    background-position: 1440px 0;
  }
}

/* 響應式設計 */
@media (max-width: 1024px) {
  .about-container {
    padding: 2rem;
  }

  .content-block,
  .content-block.reverse {
    flex-direction: column;
    gap: 2rem;
  }

  .text-content,
  .image-wrapper {
    width: 100%;
    padding: 1rem;
  }
}

@media (max-width: 768px) {

  .d-flex {
    flex-direction: column;
  }
  .main-title {
    font-size: 2.5rem;
  }

  .page-header {
    padding: 2rem;
  }
}
</style>