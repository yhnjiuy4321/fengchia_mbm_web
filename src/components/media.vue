<script setup>
import { mediaContent } from "@/data/homepage/media.js";
const media = mediaContent;
</script>

<template>
  <div class="media-section">
    <div class="section-header">
      <h1>媒體影音</h1>
      <div class="header-line"></div>
    </div>

    <div class="media-container">
      <div v-for="item in media" :key="item.id" class="media-content">
        <!-- 影片區域 -->
        <div class="video-container">
          <div class="video-wrapper">
            <iframe
                :src="item.video"
                style="border: none;"
                allowfullscreen
                loading="lazy">
            </iframe>
          </div>
        </div>

        <!-- 海報輪播 -->
        <div class="poster-carousel">
          <div :id="`posterCarousel${item.id}`" class="carousel slide carousel-fade"
               data-bs-ride="carousel" data-bs-interval="500">
            <!-- 指示器 -->
            <div class="carousel-indicators">
              <button v-for="(poster, index) in item.poster"
                      :key="index"
                      type="button"
                      :class="['indicator-btn', { active: index === 0 }]"
                      :data-bs-target="`#posterCarousel${item.id}`"
                      :data-bs-slide-to="index"
                      :aria-label="`Slide ${index + 1}`">
              </button>
            </div>

            <!-- 輪播內容 -->
            <div class="carousel-inner">
              <div v-for="(poster, index) in item.poster"
                   :key="poster.id"
                   :class="['carousel-item', { active: index === 0 }]">
                <img :src="poster.img" class="d-block w-100" :alt="`Poster ${index + 1}`">
                <div class="poster-overlay"></div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.media-section {
  padding: 4rem 2rem;
  background: #006994FF;
  min-height: 100vh;
}

.section-header {
  text-align: center;
  margin-bottom: 3rem;
}

.section-header h1 {
  color: #fff;
  font-size: 3rem;
  font-weight: 600;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
  margin-bottom: 1rem;
}

.header-line {
  width: 100px;
  height: 3px;
  background: linear-gradient(90deg, transparent, #b3e0ff, transparent);
  margin: 0 auto;
}

.media-container {
  max-width: 1400px;
  margin: 0 auto;
}

.media-content {
  display: flex;
  gap: 2rem;
  margin-bottom: 3rem;
}

.video-container {
  flex: 1;
  background: rgba(255, 255, 255, 0.1);
  border-radius: 20px;
  overflow: hidden;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
}

.video-wrapper {
  position: relative;
  padding-top: 56.25%; /* 16:9 寬高比 */
}

.video-wrapper iframe {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  border-radius: 20px;
}

.poster-carousel {
  flex: 1;
  border-radius: 20px;
  overflow: hidden;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
  background: rgba(255, 255, 255, 0.1);
}

.carousel {
  width: 100%;
  height: 100%;
}

.carousel-inner {
  height: 100%;
  border-radius: 20px;
  overflow: hidden;
}

.carousel-item {
  height: 100%;
  position: relative;
}

.carousel-item img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.5s ease;
}

.poster-overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}

.carousel-indicators {
  bottom: 20px;
}

.indicator-btn {
  width: 12px;
  height: 12px;
  border-radius: 50%;
  border: 2px solid #fff;
  background: transparent;
  margin: 0 5px;
  transition: all 0.3s ease;
}

.indicator-btn {
  background: #fff;
  transform: scale(1.2);
}

/* 懸停效果 */
.carousel-item:hover img {
  transform: scale(1.05);
}

/* 響應式設計 */
@media (max-width: 992px) {
  .media-content {
    flex-direction: column;
  }

  .video-wrapper {
    padding-top: 75%; /* 4:3 比例，更適合移動設備 */
  }

  .poster-carousel {
    height: 400px;
  }
}

@media (max-width: 768px) {
  .section-header h1 {
    font-size: 2.5rem;
  }

  .media-section {
    padding: 3rem 1rem;
  }

  .poster-carousel {
    height: 300px;
  }
}

@media (max-width: 576px) {
  .section-header h1 {
    font-size: 2rem;
  }

  .poster-carousel {
    height: 250px;
  }

  .video-wrapper {
    padding-top: 100%; /* 1:1 比例，更適合小螢幕 */
  }
}
</style>