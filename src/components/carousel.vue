<script setup>
import { carousel_img } from "@/data/homepage/carousel_img.js";
const carousel = carousel_img;
</script>

<template>
  <div id="titleCarousel" class="carousel slide" data-bs-ride="carousel" data-bs-interval="3000">
    <!-- 指示器 -->
    <div class="carousel-indicators">
      <button v-for="(item, index) in carousel"
              :key="index"
              type="button"
              :class="['indicator-btn', { active: index === 0 }]"
              :aria-current="index === 0"
              data-bs-target="#titleCarousel"
              :data-bs-slide-to="index"
              :aria-label="`Slide ${index + 1}`">
      </button>
    </div>

    <div class="carousel-inner">
      <div v-for="(Item, index) in carousel"
           :key="Item.id"
           :class="['carousel-item', { active: index === 0 }]">
        <div class="image-overlay"></div>
        <img :src="Item.img" class="d-block w-100" :alt="'Slide ' + (index + 1)">
      </div>
    </div>

    <button class="carousel-control-prev custom-control" type="button" data-bs-target="#titleCarousel" data-bs-slide="prev">
      <span class="carousel-control-prev-icon" aria-hidden="true"></span>
      <span class="visually-hidden">Previous</span>
    </button>

    <button class="carousel-control-next custom-control" type="button" data-bs-target="#titleCarousel" data-bs-slide="next">
      <span class="carousel-control-next-icon" aria-hidden="true"></span>
      <span class="visually-hidden">Next</span>
    </button>
  </div>
</template>

<style scoped>
.carousel {
  margin-top: 80px;
  width: 100%;
  height: 450px; /* 調整為與 carousel-item 一致的高度 */
  position: relative;
  overflow: hidden;
}

.carousel-item {
  height: 450px;
  position: relative;
  overflow: hidden; /* 防止圖片溢出 */
}

.image-overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: linear-gradient(rgba(0, 0, 0, 0.2), rgba(0, 0, 0, 0.5));
  z-index: 1;
}

.carousel-item img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: center; /* 確保圖片居中顯示 */
  transform: scale(1.1);
  transition: transform 0.5s ease;
}

.carousel-item.active img {
  transform: scale(1);
}

.carousel-caption {
  position: absolute;
  bottom: 20%;
  left: 50%;
  transform: translateX(-50%);
  z-index: 2;
  text-align: center;
  background: rgba(0, 40, 85, 0.6);
  padding: 2rem 4rem;
  border-radius: 15px;
  backdrop-filter: blur(5px);
}

.carousel-caption h1 {
  font-size: 3.2em;
  font-weight: 600;
  color: #fff;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5);
  margin-bottom: 0.5rem;
}

.caption-line {
  width: 50px;
  height: 3px;
  background: #fff;
  margin: 1rem auto 0;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.3);
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

.indicator-btn.active {
  background: #fff;
  transform: scale(1.2);
}

.custom-control {
  width: 5%;
  height: 100%;
  opacity: 0;
  transition: opacity 0.3s ease;
}

.carousel:hover .custom-control {
  opacity: 1;
}

.carousel-control-prev-icon,
.carousel-control-next-icon {
  background-color: rgba(0, 40, 85, 0.7);
  border-radius: 50%;
  padding: 2rem;
}



@media (max-width: 1200px) {
  .carousel-caption h1 {
    font-size: 2.8em;
  }
}

@media (max-width: 992px) {
  .carousel {
    height: 500px;
  }
  .carousel-item {
    height: 500px;
  }
  .carousel-caption h1 {
    font-size: 2.4em;
  }
  .carousel-caption {
    padding: 1.5rem 3rem;
  }
}

@media (max-width: 768px) {
  .carousel {
    height: 400px;
  }
  .carousel-item {
    height: 400px;
  }
  .carousel-caption h1 {
    font-size: 2em;
  }
  .carousel-caption {
    padding: 1rem 2rem;
  }
}

@media (max-width: 576px) {
  .carousel {
    height: 300px;
  }
  .carousel-item {
    height: 300px;
  }
  .carousel-caption h1 {
    font-size: 1.6em;
  }
  .carousel-caption {
    padding: 0.8rem 1.5rem;
  }
}
</style>