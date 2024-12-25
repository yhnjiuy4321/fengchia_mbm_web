<script setup>
import pagehead from '@/components/header.vue'
import pagefooter from '@/components/footer.vue'
import carouselComponent from '@/components/carousel.vue'
import menuComponent from '@/components/NavMenu.vue'
import axios from "axios";
import {ref} from "vue";


const userInput = ref('')
const ticket = ref({})

function searchGo() {
  axios.get(`http://localhost:5001/api/data/ticket/${userInput.value}`)
    .then(response => {
      if (response.data.length === 0) {
        console.error('No ticket found')
        // Show the modal
        //抓取modal的id
        const modal = new bootstrap.Modal(document.getElementById('noSearch'), { backdrop: true })
        modal.show()
      } else {
        ticket.value = response.data[0]
        console.log('ticket:', ticket.value)
        //把visit_date和purchase_time轉換成日期格式
        ticket.value.visit_date = new Date(ticket.value.visit_date).toLocaleDateString()
        ticket.value.purchase_time = new Date(ticket.value.purchase_time).toLocaleDateString()

        //總金額
        ticket.value.totalPrice = ticket.value.adultTicket * 300 + ticket.value.childTicket * 150 + ticket.value.elderlyTicket * 130


        // Show the modal
        //抓取modal的id
        const modal = new bootstrap.Modal(document.getElementById('haveSearch'), { backdrop: true })
        modal.show()
      }
    })
    .catch(error => {
      console.error('Error fetching ticket data:', error)
    })
}
</script>

<template>
  <pagehead/>
  <carouselComponent/>
  <div class="d-flex mt-5">
    <menuComponent/>

    <div class="page-container">
      <!-- 查詢區塊 -->
      <div class="search-container">
        <div class="search-header">
          <div class="header-icon">🎫</div>
          <h2>訂票查詢</h2>
          <p class="subtitle">查詢您的訂票資訊</p>
        </div>

        <div class="search-box">
          <div class="input-group">
            <span class="input-icon">🔎</span>
            <input
                type="text"
                v-model="userInput"
                placeholder="請輸入手機號碼、身分證、訂單編號（三擇一）"
                class="search-input"
            >
          </div>
          <button @click="searchGo" class="search-button">
            <span v-if="!loading">查詢訂票</span>
            <span v-else class="loading-spinner"></span>
          </button>
        </div>

        <div class="search-tips">
          <div class="tip-item">
            <span class="tip-icon">📱</span>
            <span>手機號碼</span>
          </div>
          <div class="tip-item">
            <span class="tip-icon">📋</span>
            <span>身分證字號</span>
          </div>
          <div class="tip-item">
            <span class="tip-icon">🔢</span>
            <span>訂單編號</span>
          </div>
        </div>
      </div>
    </div>
  </div>

  <!-- 查詢結果 Modal -->
  <div class="modal fade" id="haveSearch">
    <div class="modal-dialog">
      <div class="modal-content">
        <div class="modal-header">
          <h4 class="modal-title">
            <span class="modal-icon">🎫</span>
            訂票資訊
          </h4>
          <button type="button" class="btn-close" data-bs-dismiss="modal"></button>
        </div>

        <div class="modal-body">
          <div class="ticket-info">
            <div class="info-group">
              <div class="info-label">訂票人</div>
              <div class="info-value">{{ ticket.name }}</div>
            </div>
            <div class="info-group">
              <div class="info-label">聯絡電話</div>
              <div class="info-value">{{ ticket.phone }}</div>
            </div>
            <div class="info-group">
              <div class="info-label">參觀日期</div>
              <div class="info-value">{{ ticket.visit_date }}</div>
            </div>
            <div class="info-group">
              <div class="info-label">購票日期</div>
              <div class="info-value">{{ ticket.purchase_time }}</div>
            </div>
            <div class="ticket-details">
              <div class="ticket-type">
                <span class="type-label">全票</span>
                <span class="type-count">{{ ticket.adultTicket }}張</span>
              </div>
              <div class="ticket-type">
                <span class="type-label">兒童票</span>
                <span class="type-count">{{ ticket.childTicket }}張</span>
              </div>
              <div class="ticket-type">
                <span class="type-label">敬老票</span>
                <span class="type-count">{{ ticket.elderlyTicket }}張</span>
              </div>
            </div>
            <div class="total-price">
              <span>總金額</span>
              <span class="price">NT$ {{ ticket.totalPrice }}</span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>

  <!-- 查無結果 Modal -->
  <div class="modal fade" id="noSearch">
    <div class="modal-dialog">
      <div class="modal-content">
        <div class="modal-header">
          <h4 class="modal-title">查詢結果</h4>
          <button type="button" class="btn-close" data-bs-dismiss="modal"></button>
        </div>

        <div class="modal-body">
          <div class="no-result">
            <div class="error-icon">❌</div>
            <h3>查無訂票資訊</h3>
            <p>請確認輸入資訊是否正確，或聯絡客服人員協助。</p>
            <button class="support-button" data-bs-dismiss="modal">
              聯絡客服
            </button>
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
  min-height: 80vh;
  padding: 3rem;
  background: #f8fcff;
  display: flex;
  justify-content: center;
  align-items: center;
}

.search-container {
  width: 100%;
  max-width: 800px;
  background: white;
  border-radius: 20px;
  padding: 3rem;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
}

.search-header {
  text-align: center;
  margin-bottom: 2rem;
}

.header-icon {
  font-size: 3rem;
  margin-bottom: 1rem;
}

.search-header h2 {
  color: #1a4c7c;
  font-size: 2.5rem;
  font-weight: 700;
  margin-bottom: 0.5rem;
}

.subtitle {
  color: #666;
  font-size: 1.1rem;
}

.search-box {
  margin-bottom: 2rem;
}

.input-group {
  position: relative;
  margin-bottom: 1.5rem;
}

.input-icon {
  position: absolute;
  left: 1rem;
  top: 50%;
  transform: translateY(-50%);
  font-size: 1.2rem;
  color: #1a4c7c;
}

.search-input {
  width: 100%;
  padding: 1rem 1rem 1rem 3rem;
  border: 2px solid #e0e0e0;
  border-radius: 10px;
  font-size: 1.1rem;
  transition: all 0.3s ease;
}

.search-input:focus {
  border-color: #1a4c7c;
  outline: none;
  box-shadow: 0 0 0 3px rgba(26, 76, 124, 0.1);
}

.search-button {
  width: 100%;
  padding: 1rem;
  background: linear-gradient(135deg, #1a4c7c 0%, #2980b9 100%);
  color: white;
  border: none;
  border-radius: 10px;
  font-size: 1.1rem;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
}

.search-button:hover {
  transform: translateY(-2px);
  box-shadow: 0 4px 15px rgba(26, 76, 124, 0.3);
}

.search-tips {
  display: flex;
  justify-content: center;
  gap: 2rem;
  margin-top: 2rem;
}

.tip-item {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  color: #666;
}

/* Modal 樣式 */
.modal-content {
  border-radius: 15px;
  overflow: hidden;
}

.modal-header {
  background: #1a4c7c;
  color: white;
  padding: 1.5rem;
}

.modal-title {
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.ticket-info {
  padding: 1rem;
}

.info-group {
  display: flex;
  margin-bottom: 1rem;
  padding: 0.5rem;
  background: #f8fcff;
  border-radius: 8px;
}

.info-label {
  flex: 0 0 100px;
  color: #1a4c7c;
  font-weight: 600;
}

.info-value {
  flex: 1;
}

.ticket-details {
  margin-top: 1.5rem;
  padding: 1rem;
  background: #f0f7ff;
  border-radius: 10px;
}

.ticket-type {
  display: flex;
  justify-content: space-between;
  margin-bottom: 0.5rem;
}

.total-price {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-top: 1.5rem;
  padding: 1rem;
  background: #1a4c7c;
  color: white;
  border-radius: 10px;
  font-size: 1.2rem;
  font-weight: 600;
}

.no-result {
  text-align: center;
  padding: 2rem;
}

.error-icon {
  font-size: 4rem;
  margin-bottom: 1rem;
  color: #dc3545;
}

.support-button {
  margin-top: 1rem;
  padding: 0.75rem 2rem;
  background: #1a4c7c;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: all 0.3s ease;
}

.support-button:hover {
  background: #2980b9;
}

@keyframes spin {
  to {
    transform: rotate(360deg);
  }
}

.loading-spinner {
  display: inline-block;
  width: 20px;
  height: 20px;
  border: 3px solid #fff;
  border-radius: 50%;
  border-top-color: transparent;
  animation: spin 1s linear infinite;
}

@media (max-width: 800px) {

  .d-flex {
    flex-direction: column;
    gap: 2rem;
  }

  .search-container {
    padding: 2rem;
  }

  .search-header h2 {
    font-size: 2rem;
  }

  .subtitle {
    font-size: 1rem;
  }

  .input-icon {
    font-size: 1rem;
  }

  .search-input {
    font-size: 1rem;
  }

  .search-button {
    font-size: 1rem;
  }

  .search-tips {
    flex-direction: row;
    gap: 1rem;
  }

  .tip-item {
    font-size: 0.9rem;
  }

  .modal-title {
    font-size: 1.5rem;
  }

  .info-label {
    font-size: 0.9rem;
  }

  .info-value {
    font-size: 0.9rem;
  }

  .ticket-details {
    font-size: 0.9rem;
  }

  .ticket-type {
    font-size: 0.9rem;
  }

  .total-price {
    font-size: 1rem;
  }

  .error-icon {
    font-size: 3rem;
  }

  .support-button {
    font-size: 0.9rem;
  }

}
</style>