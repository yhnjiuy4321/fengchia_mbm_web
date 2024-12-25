<script setup>
// 可以添加當前年份
const currentYear = new Date().getFullYear()
</script>

<template>
  <footer class="footer">
    <div class="waves">
      <div class="wave" id="wave1"></div>
      <div class="wave" id="wave2"></div>
      <div class="wave" id="wave3"></div>
      <div class="wave" id="wave4"></div>
    </div>

    <div class="footer-content">
      <div class="footer-title">
        <span class="chinese">逢甲海洋生物博物館</span>
        <span class="english">Feng Chia Marine Biology Museum</span>
      </div>

      <div class="footer-info">
        <div class="info-item">
          <i class="fas fa-phone"></i>
          電話：06-267840
        </div>
        <div class="info-item">
          <i class="fas fa-envelope"></i>
          Email：fcmbm1234@welcome.com
        </div>
      </div>

      <div class="copyright">
        © {{ currentYear }} Copyright Feng Chia Marine Biology Museum. All Rights Reserved.
      </div>
    </div>
  </footer>
</template>

<style scoped>
.footer {

  position: relative;
  background: linear-gradient(to right, #006994, #003a61);
  min-height: 200px;
  padding: 3rem 2rem 2rem;
  color: #fff;
  overflow: hidden;
}

/* 波浪動畫 */
.waves {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100px;
  overflow: hidden;
}

.wave {
  position: absolute;
  top: -60px;
  left: 0;
  width: 200%;
  height: 100px;
  background: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 800 88.7'%3E%3Cpath d='M800 56.9c-155.5 0-204.9-50-405.5-49.9-200 0-250 49.9-394.5 49.9v31.8h800v-.2-31.6z' fill='rgba(255, 255, 255, 0.1)'/%3E%3C/svg%3E");
  background-size: 50% 100px;
  animation: wave 15s linear infinite;
}

#wave1 {
  z-index: 1;
  opacity: 0.7;
  animation-delay: 0s;
}

#wave2 {
  z-index: 2;
  opacity: 0.5;
  animation-delay: -5s;
}

#wave3 {
  z-index: 3;
  opacity: 0.3;
  animation-delay: -2s;
}

#wave4 {
  z-index: 4;
  opacity: 0.2;
  animation-delay: -7s;
}

@keyframes wave {
  0% { transform: translateX(0) translateZ(0) scaleY(1); }
  50% { transform: translateX(-25%) translateZ(0) scaleY(0.8); }
  100% { transform: translateX(-50%) translateZ(0) scaleY(1); }
}

.footer-content {
  position: relative;
  z-index: 5;
  max-width: 1200px;
  margin: 0 auto;
  text-align: center;
}

.footer-title {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-bottom: 2rem;
}

.footer-title .chinese {
  font-size: 1.8rem;
  font-weight: 600;
  margin-bottom: 0.5rem;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
}

.footer-title .english {
  font-size: 1.2rem;
  color: rgba(255, 255, 255, 0.9);
}

.footer-info {
  display: flex;
  justify-content: center;
  gap: 3rem;
  margin-bottom: 2rem;
}

.info-item {
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.info-item i {
  color: #b3e0ff;
}

.copyright {
  padding-top: 2rem;
  border-top: 1px solid rgba(255, 255, 255, 0.2);
  font-size: 0.9rem;
  color: rgba(255, 255, 255, 0.8);
}

/* 響應式設計 */
@media (max-width: 768px) {
  .footer {
    padding: 2rem 1rem 1.5rem;
  }

  .footer-title .chinese {
    font-size: 1.5rem;
  }

  .footer-title .english {
    font-size: 1rem;
  }

  .footer-info {
    flex-direction: column;
    gap: 1rem;
  }

  .info-item {
    justify-content: center;
  }
}

/* 懸停效果 */
.info-item:hover {
  color: #b3e0ff;
  transform: translateY(-2px);
  transition: all 0.3s ease;
}

.info-item:hover i {
  animation: pulse 1s infinite;
}

@keyframes pulse {
  0% { transform: scale(1); }
  50% { transform: scale(1.2); }
  100% { transform: scale(1); }
}
</style>