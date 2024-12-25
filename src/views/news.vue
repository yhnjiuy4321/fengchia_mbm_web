<script setup>
import pagehead from '@/components/header.vue'
import pagefooter from '@/components/footer.vue'
import carouselComponent from '@/components/carousel.vue'
import menuComponent from '@/components/NavMenu.vue'
import router from "@/router/index.js";

const goToArticle = (id) => {
  console.log('go to article')
  router.push(`/homepage/News/article/${id}`)
}

import {ref} from "vue";
import { newsContent } from '../data/newsContent.js'
import { venusContent } from '../data/newsContent.js'
const forNews = ref(newsContent)
const forVenus = ref(venusContent)

//反轉陣列(時間由新到舊)
//forNews.value.reverse()
//forVenus.value.reverse()

window.scrollTo(0,0);//來到此頁面時，將滾動條移動到最上方
</script>

<template>

  <pagehead/>
  <carouselComponent/>

  <div class="d-flex mt-5">
    <menuComponent/>
    <div class="news_container w-100 p-5">

      <div class="selectBar mb-3">
        <ul class="nav nav-tabs" id="myTab" role="tablist">
          <li class="nav-item" role="presentation">
            <a class="nav-link active " id="field-tab" data-bs-toggle="tab" href="#field" role="tab" aria-controls="field"
               aria-selected="true">場館消息</a>
          </li>
          <li class="nav-item" role="presentation">
            <a class="nav-link" id="report-tab" data-bs-toggle="tab" href="#report" role="tab" aria-controls="report"
               aria-selected="false">相關報導</a>
          </li>
        </ul>
      </div>

      <!-- 選項卡內容 -->
      <div class="tab-content" id="myTabContent">

        <!--場館資訊-->
        <div class="tab-pane fade show active" id="field" role="tabpanel" aria-labelledby="field-tab">
          <div class="content">
            <table class="table table-striped w-100">
              <thead>
              <tr class="title">
                <td class="date">發布日期</td>
                <td class="article">內容</td>
              </tr>
              </thead>
              <tbody v-for="item in forVenus" :key="item.id">
              <tr>
                <td>{{item.date}}</td>
                <td>
                  <a @click="goToArticle(item.id)">{{item.title}}</a>
                </td>
              </tr>
              </tbody>
            </table>
          </div>
        </div>

        <div class="tab-pane fade" id="report" role="tabpanel" aria-labelledby="report-tab">
          <div class="content">
            <table class="table table-striped w-100">
              <thead>
              <tr class="title">
                <td class="date">發布日期</td>
                <td class="article">內容</td>
              </tr>
              </thead>
              <tbody v-for="item in forNews" :key="item.id">
              <tr>
                <td>{{item.date}}</td>
                <td>
                  <a @click="goToArticle(item.id)">{{item.title}}</a>
                </td>
              </tr>
              </tbody>
            </table>
          </div>
        </div>
      </div>
    </div>
  </div>

  <pagefooter/>


</template>

<style scoped>
/* 主容器樣式 */
.news_container {
  background: rgba(119, 178, 239, 0.5);
  border-radius: 20px;
  min-height: 100vh;
  box-shadow: 0 8px 32px rgba(31, 38, 135, 0.15);
  padding: 2rem;
  position: relative;
  overflow: hidden;
  margin: 2rem;
}
/* 添加裝飾性波浪背景 */
.news_container::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: url("data:image/svg+xml,%3Csvg width='60' height='60' viewBox='0 0 60 60' xmlns='http://www.w3.org/2000/svg'%3E%3Cpath d='M30 60c16.569 0 30-13.431 30-30C60 13.431 46.569 0 30 0 13.431 0 0 13.431 0 30c0 16.569 13.431 30 30 30zm0-5c13.807 0 25-11.193 25-25S43.807 5 30 5 5 16.193 5 30s11.193 25 25 25z' fill='%23FFFFFF' fill-opacity='0.1'/%3E%3C/svg%3E") repeat;
  opacity: 0.1;
  z-index: -1;
}

/* 標題區域美化 */
.selectBar {
  position: relative;
  margin-bottom: 2rem;
}

/* 選項卡樣式 */
.nav-tabs {
  border: none;
  background: rgba(119, 178, 239, 0.3);
  border-radius: 15px;
  padding: 0.8rem;
  display: flex;
  gap: 1rem;
}

.nav-link {
  position: relative;
  padding: 1rem 2rem;
  border-radius: 12px !important;
  transition: all 0.3s ease;
  font-weight: 600;
  overflow: hidden;
}
/* 添加標籤懸停效果 */
.nav-link::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: linear-gradient(45deg, rgba(255,255,255,0.2), rgba(255,255,255,0));
  transform: translateX(-100%);
  transition: transform 0.3s ease;
}

.nav-link:hover::before {
  transform: translateX(0);
}
.nav-link:hover {
  background: rgba(119, 178, 239, 0.9);
}

.nav-link.active {
  background: #1a3778 !important; /* 與選單相同的藍色 */
  color: #ffffff !important;
}

/* 表格樣式 */
.table {
  background: rgba(255, 255, 255, 0.9);
  border-radius: 15px;
  overflow: hidden;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
}

.title td {
  background: #77b2ef !important;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 1px;
  position: relative;
  text-align: center;
}

tbody tr {
  position: relative;
  transition: all 0.3s ease;
}

tbody tr:hover {
  transform: translateX(5px);
  background: rgb(255, 255, 255);
}

td {
  padding: 1rem !important;
  color: #333333;
  border: none !important;
  text-align: center;
}

tbody td a {
  display: block;
  position: relative;
  overflow: hidden;
}

tbody td a:hover {
  color: #0088cc;
  border-bottom: 2px solid #0088cc;
  cursor: pointer;
  font-weight: 700;
}
/* 添加連結懸停效果 */
tbody td a::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 0;
  width: 100%;
  height: 2px;
  background: #0088cc;
  transform: scaleX(0);
  transform-origin: left;
  transition: transform 0.3s ease;
}

tbody td a:hover::after {
  transform: scaleX(1);
}

/* 添加陰影效果 */
.table {
  position: relative;
}

.table::after {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  box-shadow: inset 0 0 20px rgba(0, 0, 0, 0.05);
  pointer-events: none;
  border-radius: 15px;
}

/* 日期欄位樣式 */
.date {
  position: relative;
  font-family: 'Roboto Mono', monospace;
  color: #1a4c7c;
}

/* 添加響應式動畫 */
@media (max-width: 768px) {
  tbody tr:hover {
    transform: none;
  }

  .nav-tabs {
    justify-content: space-around;
    gap: 1rem;
  }
  .nav-link {
    padding: 0.8rem 1.5rem;
  }

  .table::after {
    box-shadow: none;
  }

  .d-flex {
    flex-direction: column;
  }

  .news_container {
    margin: 0 0 1rem;
  }
}
</style>