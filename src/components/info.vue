<script setup>
import { intro } from "@/data/homepage/sampleIntro.js";
const introContent = intro;
</script>

<template>
  <div v-for="intro in introContent" :key="intro.id" class="info-container">
    <div class="content-wrapper">
      <div class="info-card openTime">
        <div class="info-content time">
          <div class="icon-container">
            <i class="fas fa-clock"></i>
          </div>
          <h2>開館時間</h2>
          <div class="divider"></div>
          <p>{{intro.day}}</p>
          <p>{{intro.time}}</p>
        </div>
        <div class="photo-container">
          <img src="@/assets/photo/1.png" alt="開館時間照片">
          <div class="photo-overlay"></div>
        </div>
      </div>

      <div class="info-card address">
        <div class="photo-container">
          <img src="@/assets/photo/2.png" alt="地址照片">
          <div class="photo-overlay"></div>
        </div>
        <div class="info-content location">
          <div class="icon-container">
            <i class="fas fa-map-marker-alt"></i>
          </div>
          <h2>本館地址</h2>
          <div class="divider"></div>
          <p>{{intro.address}}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.info-container {
  padding: 4rem 2rem;
  background: linear-gradient(135deg, #006994 0%, #003a61 100%);
  min-height: 100vh;
  display: flex;
  align-items: center;
}

.content-wrapper {
  max-width: 1200px;
  margin: 0 auto;
  width: 100%;
}

.info-card {
  display: flex;
  background: rgba(255, 255, 255, 0.1);
  border-radius: 20px;
  overflow: hidden;
  margin: 2rem 0;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
  transition: transform 0.3s ease;
}

.info-card:hover {
  transform: translateY(-10px);
}

.info-content {
  flex: 1;
  padding: 3rem;
  background: rgba(0, 40, 85, 0.8);
  backdrop-filter: blur(10px);
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  color: white;
}

.icon-container {
  font-size: 2.5rem;
  color: #b3e0ff;
  margin-bottom: 1rem;
}

h2 {
  font-size: 2.5rem;
  font-weight: 600;
  margin-bottom: 1rem;
  color: #fff;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
}

.divider {
  width: 60px;
  height: 3px;
  background: #b3e0ff;
  margin: 1rem 0;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
}

p {
  font-size: 1.2rem;
  margin: 0.5rem 0;
  color: #e6f3ff;
  text-align: center;
}

.photo-container {
  flex: 1;
  position: relative;
  overflow: hidden;
}

.photo-container img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.5s ease;
}

.photo-overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: linear-gradient(rgba(0, 0, 0, 0.2), rgba(0, 0, 0, 0.4));
}

.info-card:hover .photo-container img {
  transform: scale(1.1);
}

@media (max-width: 992px) {
  .info-card {
    flex-direction: column;
  }

  .info-content {
    padding: 2rem;
  }

  .photo-container {
    height: 300px;
  }

  h2 {
    font-size: 2rem;
  }

  p {
    font-size: 1.1rem;
  }
}

@media (max-width: 576px) {
  .info-container {
    padding: 2rem 1rem;
  }

  h2 {
    font-size: 1.8rem;
  }

  p {
    font-size: 1rem;
  }

  .photo-container {
    height: 200px;
  }
}
</style>