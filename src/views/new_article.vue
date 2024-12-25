<script setup>
import pagehead from '@/components/header.vue'
import pagefooter from '@/components/footer.vue'
import carouselComponent from '@/components/carousel.vue'
import menuComponent from '@/components/NavMenu.vue'

import { ref } from 'vue';
import { newsContent, venusContent } from '../data/newsContent.js';
import { useRoute } from 'vue-router';

const route = useRoute();
const articleId =route.params.id; // 將 ID 轉換為數字
const forNewArticle = ref([...newsContent, ...venusContent].find(article => article.id === articleId));

const title = forNewArticle.value?.title || '文章未找到';
const date = forNewArticle.value?.date || '';
const content = forNewArticle.value?.content || '';


window.scrollTo(0,0);//來到此頁面時，將滾動條移動到最上方
</script>

<template>
  <pagehead/>
  <carouselComponent/>

  <div class="d-flex mt-5">
    <menuComponent/>

    <div class="container">
      <div class="title text-center">
        <h2>{{title}}</h2>
        <div class="date text-end">
          <p>{{date}}</p>
        </div>
      </div>
      <div class="content mt-3 p-5">
        <p>{{content}}</p>
      </div>
    </div>
  </div>

  <pagefooter/>

</template>

<style scoped>
.container {
  background: linear-gradient(135deg, rgba(0, 119, 182, 0.95) 0%, rgba(3, 4, 94, 0.9) 100%);
  border-radius: 20px;
  padding: 2rem 3rem;
  box-shadow: 0 8px 32px rgba(31, 38, 135, 0.15);
  backdrop-filter: blur(10px);
  color: #e6f3ff;
  margin: 2rem;
}

.title {
  position: relative;
  padding-bottom: 2rem;
  margin-bottom: 2rem;
}

.title h2 {
  color: #ffffff;
  font-size: 2.2rem;
  font-weight: 700;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.2);
  margin-bottom: 1rem;
}

.title::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  height: 3px;
  background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.5), transparent);
}

.date {
  color: #b3e0ff;
  font-size: 0.9rem;
  font-style: italic;
}

.content {
  background: rgba(255, 255, 255, 0.1);
  border-radius: 15px;
  padding: 2rem;
  line-height: 1.8;
  text-align: justify;
}

.content p {
  margin: 0;
  color: #e6f3ff;
}

@media (max-width: 768px) {

  .d-flex {
    flex-direction: column;
    align-items: center;
  }

  .container {
    margin: 20px;
  }
}

</style>