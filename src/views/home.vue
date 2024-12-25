<script setup>
import pagehead from '@/components/header.vue'
import carouselComponent from '@/components/carousel.vue'
import menufromhome from '@/components/menuForHomePage.vue'
import mediaComponent from '@/components/media.vue'
import infoComponent from '@/components/info.vue'
import PageFooter from "@/components/footer.vue";

// 來到此頁面時，將滾動條移動到最上方
window.scrollTo(0, 0);
</script>

<template>
  <div class="background-container">
    <!-- 這個容器專門用來展示背景圖片 -->
  </div>
  <div class="content-container">
    <pagehead />
    <carouselComponent />
    <menufromhome />
    <mediaComponent />
    <infoComponent />
    <PageFooter />
  </div>
</template>

<style scoped>
.background-container {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
  z-index: -1;
}

.background-container::after {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: -1;
}

</style>
