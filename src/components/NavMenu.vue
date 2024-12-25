<script setup>
import { useRouter } from 'vue-router'
import { ref , nextTick } from 'vue'

const router = useRouter()
const pageName = router.currentRoute.value.name
const activeDropdown = ref(null)

// 定義選單數據結構
const tourMenuItems = [
  { label: '導覽簡介', section: 'tour', icon: '🏛️' },
  { label: '深海區', section: 'deep', icon: '🌊' },
  { label: '淺海區', section: 'shallow', icon: '🐠' },
  { label: '極地世界', section: 'ice', icon: '❄️' },
  { label: '鯨魚世界', section: 'whale', icon: '🐋' }
]

const serviceMenuItems = [
  { label: '場館規則與服務', route: '/homepage/service_rules', icon: '📜' },
  { label: '線上購票', route: '/homepage/ticketShop', icon: '🎟️' },
  { label: '票務查詢', route: '/homepage/searchTicket', icon: '🔍' }
]

const navItems = [
  { label: '表演活動', route: '/homepage/Show', icon: '🎭' },
  { label: '最新消息', route: '/homepage/News', icon: '📰' },
  { label: 'Q&A問答', route: '/homepage/Q&A', icon: '❓' },
  { label: '關於我們', route: '/homepage/about', icon: '👥' },
  { label: '互動專區', route: '/homepage/bioIdentiy', icon: '🎮' }
]

const toggleDropdown = (name) => {
  activeDropdown.value = activeDropdown.value === name ? null : name
}

const navigateTo = (route) => {
  router.push(route)
}

const scrollToSection = async (section) => {
  try {
    // 先導航到 VenueTour 頁面
    await router.push('/homepage/VenueTour')

    // 等待 DOM 更新
    await nextTick()

    // 確保標籤頁被激活
    const tabId = section === 'tour' ? 'tour-tab' : section === 'deep' ? 'deep-tab' : section === 'shallow' ? 'shallow-tab' : section === 'ice' ? 'ice-tab' : section === 'whale' ? 'whale-tab' : null
    const tab = document.getElementById(tabId)
    if (tab) {
      tab.click()
    }
  } catch (error) {
    console.error('Navigation error:', error)
  }
}
</script>

<template>
  <div class="menu">
    <div class="pagename">
      <span class="whatYouChoose">
        <span class="page-icon">🌊</span>
        {{ pageName }}
      </span>
    </div>

    <nav class="navbar">
      <div class="container-fluid">
        <ul class="navbar-nav">
          <!-- 場館導覽下拉選單 -->
          <li class="menu-group">
            <button
                class="menu-button"
                :class="{ active: activeDropdown === 'tour' }"
                @click="toggleDropdown('tour')"
            >
              <span class="icon">🏛️</span>
              場館導覽
              <span class="arrow" :class="{ rotated: activeDropdown === 'tour' }">▾</span>
            </button>
            <ul class="submenu" :class="{ show: activeDropdown === 'tour' }">
              <li v-for="item in tourMenuItems" :key="item.section">
                <a
                    class="submenu-item"
                    @click.prevent="scrollToSection(item.section)"
                >
                  <span class="icon">{{ item.icon }}</span>
                  {{ item.label }}
                </a>
              </li>
            </ul>
          </li>

          <!-- 售票與服務下拉選單 -->
          <li class="menu-group">
            <button
                class="menu-button"
                :class="{ active: activeDropdown === 'service' }"
                @click="toggleDropdown('service')"
            >
              <span class="icon">🎟️</span>
              售票與服務
              <span class="arrow" :class="{ rotated: activeDropdown === 'service' }">▾</span>
            </button>
            <ul class="submenu" :class="{ show: activeDropdown === 'service' }">
              <li v-for="item in serviceMenuItems" :key="item.route">
                <a
                    class="submenu-item"
                    @click.prevent="navigateTo(item.route)"
                >
                  <span class="icon">{{ item.icon }}</span>
                  {{ item.label }}
                </a>
              </li>
            </ul>
          </li>

          <!-- 一般導航項目 -->
          <li
              v-for="item in navItems"
              :key="item.route"
              class="nav-item"
          >
            <a
                class="nav-link"
                @click.prevent="navigateTo(item.route)"
            >
              <span class="icon">{{ item.icon }}</span>
              {{ item.label }}
            </a>
          </li>
        </ul>
      </div>
    </nav>
  </div>
</template>


<style scoped>
.menu {
  display: flex;
  flex-direction: column;
  align-items: stretch;
  min-width: 25%;
  padding: 15px;
  margin: 15px;
  height: 100%;
  backdrop-filter: blur(10px);
  border-radius: 20px;
  box-shadow: 0 8px 32px rgba(31, 38, 135, 0.15);

}

.navbar {
  padding: 1rem;
  border-radius: 15px;
  background: linear-gradient(135deg, rgba(115, 183, 255, 0.2), rgba(115, 183, 255, 0.4));
  backdrop-filter: blur(5px);
}

.container-fluid {
  display: flex;
  flex-direction: column;
  width: 100%;
}

.navbar-nav {
  width: 100%;
  display: flex;
  flex-direction: column;
  gap: 10px;
  padding: 0;
  list-style: none;
}

.pagename {
  margin-bottom: 30px;
  width: 100%;
}

.whatYouChoose {
  font-size: 32px;
  color: #201f1f;
  font-weight: 900;         /*粗體*/
  padding: 25px;
  background: linear-gradient(135deg, #77b2ef, #5c9ce0);
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 15px;
  box-shadow: 0 4px 15px rgba(23, 22, 22, 0.94);
  transition: transform 0.3s ease;
  gap: 10px;
}

.whatYouChoose:hover {
  transform: translateY(-2px);
}

.page-icon {
  font-size: 28px;
}

.menu-group {
  width: 100%;
  margin-bottom: 5px;
}

.menu-button {
  width: 100%;
  padding: 12px 30px;
  border: none;
  border-radius: 12px;
  background: linear-gradient(135deg, #77b2ef, #5c9ce0);
  color: #1e1d1d;
  font-size: 16px;
  font-weight: 900;         /*粗體*/
  align-items: center;
  justify-content: space-between;
  cursor: pointer;
  transition: all 0.3s ease;
}

.menu-button:hover {
  transform: translateY(-2px);
  box-shadow: 0 4px 15px rgba(119, 178, 239, 0.3);
}

.menu-button.active {
  background: linear-gradient(135deg, #5c9ce0, #4785c9);
}

.arrow {
  transition: transform 0.3s ease;
}

.arrow.rotated {
  transform: rotate(180deg);
}

.submenu {
  max-height: 0;
  overflow: hidden;
  transition: max-height 0.3s ease-out;
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(5px);
  border-radius: 12px;
  margin-top: 5px;
  padding: 0;
  list-style: none;
}

.submenu.show {
  max-height: 300px;
}

.submenu-item {
  padding: 10px 20px;
  color: #1c1b1b;
  display: flex;
  align-items: center;
  gap: 10px;
  cursor: pointer;
  transition: background-color 0.3s ease;
  text-decoration: none; /* 移除底線 */

}

.submenu-item:hover {
  background: rgba(115, 183, 255, 0.5);
}

.nav-item {
  width: 100%;
  border-radius: 12px;
  overflow: hidden;
  background: linear-gradient(135deg, #77b2ef, #5c9ce0);
  transition: transform 0.3s ease;
}

.nav-item:hover {
  transform: translateY(-2px);
  box-shadow: 0 4px 15px rgba(119, 178, 239, 0.3);
}

.nav-link {
  color: #272626;
  text-decoration: none;
  padding: 12px 20px;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 10px;
  cursor: pointer;
  font-weight: 900;         /*粗體*/

}


.icon {
  font-size: 25px;
  display: inline-flex;
  align-items: center;
  justify-content: center;
}
/* 動畫效果 */
@keyframes slideDown {
  from {
    opacity: 0;
    transform: translateY(-10px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.submenu.show li {
  animation: slideDown 0.3s ease forwards;
}

/*響應式設計*/
@media (max-width: 768px) {

  .menu {
    min-width: 90%;
    margin: 10px

  }

  .whatYouChoose {
    font-size: 24px;
  }

  .menu-button, .nav-link {
    padding: 10px 15px;
  }
}
</style>