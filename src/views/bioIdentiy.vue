<script setup>
import pagehead from '@/components/header.vue'
import pagefooter from '@/components/footer.vue'
import carouselComponent from '@/components/carousel.vue'
import menuComponent from '@/components/NavMenu.vue'
import {marineTranslations} from '@/data/bioResult.js'

window.scrollTo(0, 0);//來到此頁面時，將滾動條移動到最上方

import {ref} from "vue";

const PORT = 5002
const imageFile = ref(null)
const imagePreview = ref(null)
const loading = ref(false)
const error = ref(null)
const results = ref(null)


const handleFileUpload = (event) => {
  const file = event.target.files[0]
  if (!file) return

  imageFile.value = file
  imagePreview.value = URL.createObjectURL(file)
  results.value = null
  error.value = null
}

const analyzeImage = async () => {
  if (!imageFile.value) return

  loading.value = true
  error.value = null
  results.value = null

  try {
    const base64Image = await getBase64(imageFile.value)

    const requestBody = {
      requests: [{
        image: {
          content: base64Image.split(',')[1]
        },
        features: [
          {type: 'LABEL_DETECTION'},      // 標籤識別
          {type: 'TEXT_DETECTION'},       // 文字識別
        ]
      }]
    }

    // 提用後端 API
    const response = await fetch(`http://localhost:${PORT}/api/analyze-image`, {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json'
      },
      body: JSON.stringify(requestBody)
    })

    if (!response.ok) {
      throw new Error('API 請求失敗')
    }

    const data = await response.json()
    results.value = data.responses[0]
  } catch (err) {
    error.value = `分析失敗: ${err.message}`
    console.error('Error:', err)
  } finally {
    loading.value = false
  }
}

const getBase64 = (file) => {
  return new Promise((resolve, reject) => {
    const reader = new FileReader()
    reader.readAsDataURL(file)
    reader.onload = () => resolve(reader.result)
    reader.onerror = error => reject(error)
  })
}


</script>

<template>
  <pagehead/>
  <carouselComponent/>
  <div class="d-flex mt-5">
    <menuComponent/>

    <div class="w-100 p-4 marine-content">
      <!-- 標題區域 -->
      <div class="page-header">
        <div class="wave-animation"></div>
        <h1 class="main-title">海洋生物辨識系統</h1>
        <p class="subtitle">運用AI技術辨識海洋生物，探索海洋世界的奧秘</p>
      </div>

      <!-- 注意事項圖片 -->
      <div class="info-section">
        <img src="@/assets/photo/ThingForBio.png" alt="上傳注意事項" class="info-image">
      </div>

      <!-- 上傳分析區域 -->
      <div class="vision-analyzer">
        <div class="upload-container">
          <div class="upload-section">
            <div class="upload-box"
                 @dragover.prevent
                 @drop.prevent="handleFileUpload">
              <input
                  type="file"
                  @change="handleFileUpload"
                  accept="image/*"
                  ref="fileInput"
                  class="file-input"
                  id="file-upload">
              <label for="file-upload" class="upload-label">
                <div class="upload-icon">🐋</div>
                <p class="upload-text">點擊或拖曳圖片到此處</p>
                <p class="upload-hint">支援 JPG, PNG 格式</p>
              </label>
            </div>


            <!-- 預覽圖片 -->
            <div v-if="imagePreview" class="preview-container">
              <img :src="imagePreview" class="preview-image">
            </div>
          </div>

          <!-- 分析按鈕 -->
          <button
              @click="analyzeImage"
              :disabled="!imageFile || loading"
              class="analyze-button">
            <span v-if="!loading">開始辨識</span>
            <span v-else class="loading-text">辨識中...</span>
          </button>

          <!-- 載入動畫 -->
          <div v-if="loading" class="loading-container">
            <div class="loading-wave"></div>
          </div>

          <!-- 錯誤訊息 -->
          <div v-if="error" class="error-message">
            <span class="error-icon">⚠️</span>
            {{ error }}
          </div>

          <!-- 辨識結果 -->
          <div v-if="results" class="results-container">
            <h3 class="results-title">
              <span class="icon">🌊</span>
              辨識結果
              <span class="icon">🌊</span>
            </h3>

            <div v-if="results.labelAnnotations">
              <!-- 主要辨識結果 -->
              <div class="primary-result">
                <h4 class="result-subtitle">最佳匹配</h4>
                <div class="scientific-name">
                  {{ marineTranslations[results.labelAnnotations[0].description] || results.labelAnnotations[0].description }}
                </div>
              </div>

              <!-- 其他結果 -->
              <div class="secondary-results">
                <h4 class="result-subtitle">其他可能的匹配</h4>
                <ul class="marine-list">
                  <template v-for="label in results.labelAnnotations" :key="label.description">
                    <li v-if="label.score >= 0.9" class="marine-item">
                      <span class="marine-name">
                        {{ marineTranslations[label.description] || label.description }}
                      </span>
                      <span class="confidence-score">
                        {{ Math.round(label.score * 100) }}%
                      </span>
                    </li>
                  </template>
                </ul>
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
.marine-content {
  background-color: #f8fcff;
}

.page-header {
  position: relative;
  background: linear-gradient(135deg, #006994 0%, #0099cc 100%);
  padding: 2rem;
  height: 130px; /* 設定你想要的具體高度 */
  border-radius: 20px;
  text-align: center;
  overflow: hidden;
  margin-bottom: 2rem;
}

.main-title {
  color: white;
  font-size: 2.5rem;
  margin-bottom: 0.5rem;
  position: relative;
  z-index: 1;
}

.subtitle {
  color: #e0f7ff;
  font-size: 1.2rem;
  position: relative;
  z-index: 1;
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

.info-section {
  text-align: center;
  margin: 2rem 0;
  padding: 0 1rem;
}

.info-image {
  max-width: 75%;
  border-radius: 15px;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s ease;
}

.info-image:hover {
  transform: scale(1.02);
}

.upload-container {
  background: white;
  border-radius: 20px;
  padding: 2rem;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.05);
}

.upload-box {
  border: 2px dashed #0099cc;
  border-radius: 15px;
  padding: 2rem;
  text-align: center;
  cursor: pointer;
  transition: all 0.3s ease;
  background: #f8fcff;
}

.upload-box:hover {
  border-color: #006994;
  background: #e6f7ff;
}

.upload-icon {
  font-size: 3rem;
  margin-bottom: 1rem;
}

.upload-text {
  font-size: 1.2rem;
  color: #006994;
  margin-bottom: 0.5rem;
}

.upload-hint {
  font-size: 0.9rem;
  color: #666;
}

.preview-container {
  margin-top: 1.5rem;
  text-align: center;
}

.preview-image {
  max-width: 100%;
  max-height: 400px;
  border-radius: 10px;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
}

.analyze-button {
  background: linear-gradient(135deg, #006994 0%, #0099cc 100%);
  color: white;
  border: none;
  padding: 1rem 3rem;
  border-radius: 30px;
  font-size: 1.1rem;
  margin: 2rem auto;
  display: block;
  transition: all 0.3s ease;
  min-width: 200px;
}

.analyze-button:not(:disabled):hover {
  transform: translateY(-2px);
  box-shadow: 0 4px 15px rgba(0, 153, 204, 0.3);
}

.analyze-button:disabled {
  background: #ccc;
  cursor: not-allowed;
}

.loading-container {
  text-align: center;
  margin: 2rem 0;
}

.loading-wave {
  display: inline-block;
  width: 50px;
  height: 50px;
  border: 3px solid #0099cc;
  border-radius: 50%;
  border-top-color: transparent;
  animation: spin 1s linear infinite;
}

.error-message {
  background: #ffe6e6;
  color: #cc0000;
  padding: 1rem;
  border-radius: 10px;
  margin: 1rem 0;
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.results-container {
  background: white;
  border-radius: 15px;
  padding: 2rem;
  margin-top: 2rem;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.05);
}

.results-title {
  color: #006994;
  text-align: center;
  font-size: 1.8rem;
  margin-bottom: 2rem;
}

.result-subtitle {
  color: #0099cc;
  margin-bottom: 1rem;
  font-size: 1.2rem;
}

.scientific-name {
  background: #e6f7ff;
  padding: 1.5rem;
  border-radius: 10px;
  font-size: 1.3rem;
  color: #006994;
  text-align: center;
  margin-bottom: 2rem;
  border-left: 5px solid #0099cc;
}

.marine-item {
  background: #f8fcff;
  padding: 1rem 1.5rem;
  border-radius: 10px;
  margin-bottom: 1rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
  transition: all 0.3s ease;
}

.marine-item:hover {
  transform: translateX(10px);
  background: rgb(117, 188, 244);
}

.confidence-score {
  background: #0099cc;
  color: white;
  padding: 0.3rem 0.8rem;
  border-radius: 20px;
  font-size: 0.9rem;
}

@keyframes wave {
  0% {
    background-position: 0 0;
  }
  100% {
    background-position: 1440px 0;
  }
}

@keyframes spin {
  to {
    transform: rotate(360deg);
  }
}

.file-input {
  display: none;
}

@media (max-width: 768px) {
  .d-flex {
    flex-direction: column;
  }

  .subtitle {
    font-size: 1rem;
  }

.info-image {
    max-width: 100%;
    border-radius: 15px;
    box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
    transition: transform 0.3s ease;
  }

  .preview-image {
    max-width: 100%;
    max-height: 300px;
    border-radius: 10px;
    box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
  }

}
</style>