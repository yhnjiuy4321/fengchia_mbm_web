<script setup>
import pagehead from '@/components/header.vue'
import pagefooter from '@/components/footer.vue'
import carouselComponent from '@/components/carousel.vue'
import menuComponent from '@/components/NavMenu.vue'
window.scrollTo(0,0);

import {ref} from "vue";
import { showContent } from '../data/showContent.js'
const forShow = ref(showContent)
</script>

<template>
  <div class="box">
    <pagehead/>
    <carouselComponent/>

    <div class="d-flex mt-5">
      <menuComponent/>

      <div class="show_container d-grid w-100 p-4">
        <div class="show_title text-center">
          <h1>每日表演活動</h1>
          <div class="title-underline"></div>
        </div>

        <div v-for="item in forShow" :key="item.id" class="show_content">
          <div class="show-card">
            <div class="image-container">
              <img :src="item.photo" alt="表演活動照片" class="show-image">
              <div class="image-overlay"></div>
            </div>

            <div class="info">
              <h2 class="show-title">{{ item.title }}</h2>
              <p class="show-intro">{{ item.intro }}</p>

              <div class="show-details">
                <div class="detail-item">
                  <i class="fas fa-calendar"></i>
                  <span>場次：{{ item.Session }}場／日</span>
                </div>

                <div class="detail-item time-slots">
                  <i class="fas fa-clock"></i>
                  <span>時間：</span>
                  <div class="time-list">
                    <span v-for="time in item.Time"
                          :key="time.id"
                          class="time-badge">
                      {{ time.time }}
                    </span>
                  </div>
                </div>

                <div class="detail-item">
                  <i class="fas fa-map-marker-alt"></i>
                  <span>地點：{{ item.Location }}</span>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
  <pagefooter/>
</template>

<style scoped>
.show_container {
  background: linear-gradient(135deg, rgba(0, 119, 182, 0.95) 0%, rgba(103, 103, 241, 0.9) 100%);
  border-radius: 20px;
  min-height: 100vh;
  box-shadow: 0 8px 32px rgba(31, 38, 135, 0.15);
  padding: 2rem;
  margin: 2rem;
}

.show_title {
  margin-bottom: 1.5rem;
  position: relative;
}

.show_title h1 {
  color: #ffffff;
  font-size: 2.5rem;
  font-weight: 700;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.2);
  margin: 0;
  padding: 1rem 2rem;
  display: inline-block;
  background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.1), transparent);
  border-radius: 15px;
}

.title-underline {
  width: 100px;
  height: 3px;
  background: linear-gradient(90deg, transparent, #ffffff, transparent);
  margin: 1rem auto 0;
}

.show-card {
  background: rgba(255, 255, 255, 0.1);
  border-radius: 20px;
  overflow: hidden;
  margin-bottom: 2rem;
  display: flex;
  position: relative;
  backdrop-filter: blur(10px);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.show-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
}

.image-container {
  width: 50%;
  position: relative;
  overflow: hidden;
}

.show-image {
  width: 100%;
  height: 400px;
  object-fit: cover;
  transition: transform 0.5s ease;
}

.show-card:hover .show-image {
  transform: scale(1.05);
}

.image-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: linear-gradient(to right, rgba(0,0,0,0), rgba(0,0,0,0.3));
}

.info {
  width: 50%;
  padding: 2rem;
  color: #ffffff;
  position: relative;
  z-index: 1;
}

.show-title {
  font-size: 3rem;
  font-weight: 700;
  margin-bottom: 1rem;
  color: #b3e0ff;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.2);
}

.show-intro {
  font-size: 1.1rem;
  line-height: 1.6;
  margin-bottom: 2rem;
  color: #e6f3ff;
}

.show-details {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.detail-item {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  color: #ffffff;
  font-weight: 600;
}

.time-slots {
  display: flex;
  align-items: flex-start;
}

.time-list {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
  margin-left: 0.5rem;
}

.time-badge {
  background: rgba(255, 255, 255, 0.2);
  padding: 0.3rem 0.8rem;
  border-radius: 20px;
  font-size: 0.9rem;
  transition: background 0.3s ease;
}

.time-badge:hover {
  background: rgba(255, 255, 255, 0.3);
}

@media (max-width: 768px) {
  .show_container {
    padding: 1rem;
    margin: 0 0 1rem;
    width: 100%;
  }

  .d-flex {
    flex-direction: column;
  }

  .show-card {
    flex-direction: column;

  }

  .image-container,
  .info {
    width: 100%;
  }

  .show-image {
    height: 300px;
  }

  .info {
    padding: 1.5rem;
  }

  .show_title h1 {
    font-size: 2rem;
  }

  .show-title {
    font-size: 1.5rem;
  }

  .show-intro {
    font-size: 1rem;
  }
}
</style>