<script setup>
import pagehead from '@/components/header.vue'
import pagefooter from '@/components/footer.vue'
import carouselComponent from '@/components/carousel.vue'
import menuComponent from '@/components/NavMenu.vue'

import {ref} from "vue";
import { Ruler } from '../data/rulerContent.js'
import { Service } from '../data/rulerContent.js'
const forRuler = ref(Ruler)
const forService = ref(Service)


</script>

<template>
  <pagehead/>
  <carouselComponent/>
  <div class="d-flex mt-5">
    <menuComponent/>
    <div class="page-container">
      <!-- 規則區塊 -->
      <div class="section-container">
        <div class="section-header">
          <div class="header-content">
            <span class="header-icon">📜</span>
            <h2>場館規則</h2>
          </div>
          <div class="header-line"></div>
        </div>

        <div class="rules-grid">
          <div v-for="item in forRuler"
               :key="item.id"
               class="rule-item">
            <div class="rule-number">{{ item.id }}</div>
            <div class="rule-content">{{ item.content }}</div>
          </div>
        </div>
      </div>

      <!-- 服務區塊 -->
      <div class="section-container">
        <div class="section-header">
          <div class="header-content">
            <span class="header-icon">🏢</span>
            <h2>場館服務</h2>
          </div>
          <div class="header-line"></div>
        </div>

        <div class="services-grid">
          <div v-for="item in forService"
               :key="item.id"
               class="service-item">
            <div class="service-number">{{ item.id }}</div>
            <div class="service-content">{{ item.content }}</div>
          </div>
        </div>
      </div>
    </div>
  </div>
  <pagefooter/>
</template>

<style scoped>
.page-container {
  width: 100%;
  padding: 2rem 4rem;
}

.section-container {
  background: white;
  border-radius: 20px;
  padding: 2rem;
  margin-bottom: 3rem;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.05);
}

.section-header {
  margin-bottom: 2rem;
  text-align: center;
}

.header-content {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 1rem;
  margin-bottom: 1rem;
}

.header-icon {
  font-size: 2rem;
}

.section-header h2 {
  color: #1a4c7c;
  font-size: 2.2rem;
  font-weight: 700;
  margin: 0;
}

.header-line {
  width: 100px;
  height: 4px;
  background: linear-gradient(to right, #1a4c7c, #2980b9);
  margin: 1rem auto 0;
  border-radius: 2px;
}

.rules-grid,
.services-grid {
  display: grid;
  gap: 1.5rem;
}

.rule-item,
.service-item {
  display: flex;
  gap: 1.5rem;
  background: #cee9fd;
  padding: 1.5rem;
  border-radius: 15px;
  transition: all 0.3s ease;
}

.rule-item:hover,
.service-item:hover {
  transform: translateX(10px);
  background: #e6f7ff;
}

.rule-number,
.service-number {
  background: #1a4c7c;
  color: white;
  width: 35px;
  height: 35px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: bold;
  flex-shrink: 0;
}

.rule-content,
.service-content {
  color: #2c3e50;
  line-height: 1.6;
  font-size: 1.1rem;
  display: flex;
  align-items: center;
}

/* 響應式設計 */
@media (max-width: 1024px) {
  .page-container {
    padding: 1.5rem;
  }

  .section-header h2 {
    font-size: 1.8rem;
  }
}

@media (max-width: 768px) {
  .rule-item,
  .service-item {
    padding: 1rem;
    gap: 1rem;
  }

  .rule-content,
  .service-content {
    font-size: 1rem;
  }

  .header-icon {
    font-size: 1.5rem;
  }
}

/* 添加漸變背景效果 */
.section-container {
  background: linear-gradient(to bottom right, rgba(232, 99, 99, 0), rgba(86, 152, 200, 0.72));
  border: 1px solid rgba(26, 76, 124, 0.1);
}

/* 添加卡片懸浮效果 */
.rule-item,
.service-item {
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.05);
}

.rule-item:hover,
.service-item:hover {
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
}

/* 序號動畫效果 */
.rule-number,
.service-number {
  transition: all 0.3s ease;
}

.rule-item:hover .rule-number,
.service-item:hover .service-number {
  transform: scale(1.1);
  background: #2980b9;
}

/* 添加分隔線 */
.rule-item:not(:last-child),
.service-item:not(:last-child) {
  border-bottom: 1px solid rgba(26, 76, 124, 0.1);
  margin-bottom: 1rem;
  padding-bottom: 1rem;
}

/* 標題裝飾 */
.section-header {
  position: relative;
  padding-bottom: 1rem;
}

.section-header::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 50%;
  transform: translateX(-50%);
  width: 150px;
  height: 2px;
  background: linear-gradient(to right, transparent, #1a4c7c, transparent);
}

@media (max-width: 768px) {
  .d-flex {
    flex-direction: column;
  }
}
</style>