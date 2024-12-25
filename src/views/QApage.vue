<script setup>
import pagehead from '@/components/header.vue'
import pagefooter from '@/components/footer.vue'
import carouselComponent from '@/components/carousel.vue'

import menuComponent from '@/components/NavMenu.vue'

window.scrollTo(0,0);//來到此頁面時，將滾動條移動到最上方

const toAquarium = () => {
  document.querySelector('.Aquarium_question').style.display = 'block'
  document.querySelector('.bio_question').style.display = 'none'
}

const tobio = () => {
  document.querySelector('.Aquarium_question').style.display = 'none'
  document.querySelector('.bio_question').style.display = 'block'
}

import {Qa_venue} from '@/data/qaContent.js';
import {Qa_bio} from '@/data/qaContent.js';
import {ref} from "vue";

const questions_venue = ref(Qa_venue);
const questions_bio = ref(Qa_bio);

</script>

<template>
  <div class="box">

    <pagehead/>
    <carouselComponent/>

    <div class="d-flex w-100 m-0 mt-5 ">
      <menuComponent/>

      <div class="question">
        <div class="btn_group d-flex">
          <div class="button-group">
            <input type="radio" id="FORchild" name="frameworks" checked="" @click="toAquarium"/>
            <label for="FORchild">場館問題</label>
          </div>

          <div class="button-group">
            <input type="radio" id="FORadult" name="frameworks" @click="tobio"/>
            <label for="FORadult">生物問題</label>
          </div>
        </div>


        <!--場館問題-->
        <div class="Aquarium_question">
          <div v-for="item in questions_venue" :key="item.id" class="question_content  w-100 p-2">
            <div class="question mt-2">
              <h2>{{ item.question }}</h2>
            </div>
            <div class="answer">
              <p class="text-start">{{ item.answer }}</p>
            </div>
          </div>
        </div>

        <!--生物問題-->
        <div class="bio_question">
          <div v-for="item in questions_bio" :key="item.id" class="question_content  w-100 p-2">
            <div class="question mt-2">
              <h2>{{ item.question }}</h2>
            </div>
            <div class="answer">
              <p class="text-start">{{ item.answer }}</p>
            </div>
          </div>
        </div>

      </div>
    </div>

    <pagefooter/>

  </div>

</template>

<style scoped>


/* 主容器樣式 */
.question {
  background: rgba(119, 178, 239, 0.5);
  border-radius: 20px;
  padding: 2rem;
  box-shadow: 0 8px 32px rgba(31, 38, 135, 0.15);
  width: 95%;  /* 減少寬度 */
  margin: 2rem;  /* 水平置中 */
  max-width: 1000px;  /* 增加最大寬度 */
}

/* 按鈕組樣式 */
.btn_group {
  display: flex;
  justify-content: center;
  gap: 1rem;
  margin-bottom: 2rem;
}

.button-group label {
  background: rgba(119, 178, 239, 0.7);
  color: #333;
  padding: 0.8rem 2rem;
  border: none;
  border-radius: 15px;
  font-weight: 600;
  font-size: 1.1rem;
  transition: all 0.3s ease;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
  width: 150px;
  text-align: center;
  position: relative;
  overflow: hidden;
  cursor: pointer;
}



.button-group label:hover {
  transform: translateY(-2px);
  background: rgb(0, 30, 110);
  color: #fff;
}


.button-group input[type="radio"] {
  display: none;
}
.button-group label {
  background: rgba(119, 178, 239, 0.7);
  color: #333;
  padding: 0.8rem 2rem;
  border: none;
  border-radius: 15px;
  font-weight: 600;
  font-size: 1.1rem;
  transition: all 0.3s ease;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
  width: 150px;
  text-align: center;
  position: relative;
  overflow: hidden;
}

/* 問答卡片樣式 */
.question_content {
  background: rgba(255, 255, 255, 0.95);
  border: none;
  border-radius: 15px;
  padding: 1.5rem !important;
  margin-bottom: 1.5rem;
  transition: transform 0.3s ease;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
}

.question_content:hover {
  transform: translateY(-5px);
}

/* 問題樣式 */
.question h2 {
  color: #1a4c7c;
  font-size: 1.2rem;
  font-weight: 700;
  margin: 0;
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.question h2::before {
  content: 'Q';
  background: #cd0d31;
  color: white;
  width: 30px;
  height: 30px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1rem;
}

/* 回答樣式 */
.answer {
  margin-top: 1.5rem;
  padding-top: 1.5rem;
  border-top: 1px solid rgb(29, 29, 30);
  position: relative;
}

.answer p {
  color: #333;
  line-height: 1.6;
  margin: 0;
  padding-left: 40px;
  position: relative;
}

.answer p::before {
  content: 'A';
  position: absolute;
  left: 0;
  top: -2px;
  background: #b3d4ff;
  color: #1a4c7c;
  width: 30px;
  height: 30px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: 700;
}

/* 切換動畫 */
.Aquarium_question,
.bio_question {
  animation: fadeIn 0.5s ease;
}

@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(10px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* 響應式設計 */
@media (max-width: 768px) {
  .d-flex {
    flex-direction: column;
  }

  .btn_group {
    flex-direction: row;
  }

  .question {
    padding: 1rem;
    margin: 12px;

  }

  .button-group label {
    padding: 0.6rem 1.5rem;
    font-size: 1rem;
    width: 120px;
  }

  .question h2 {
    font-size: 1.1rem;
  }
}
</style>