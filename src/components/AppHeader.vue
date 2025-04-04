<script setup>
import {ref} from 'vue';

const activeMenuIndex = ref(null);
const isAnyMenuActive = ref(false);

const menuItems = ref([
  {
    title: 'Collabo Platform',
    submenu: [
      {title: '시스템 소개', active: false},
      {title: '영향평가/좌표연계', active: false},
      {title: '이노폴리스 페이스', active: false},
      {title: '특허분석/활용정보', active: false},
      {title: '지역혁신역량정보', active: true}
    ]
  },
  {
    title: 'K-차트',
    submenu: [
      {title: '기업정보', active: false},
      {title: '구·특허 관리', active: false},
      {title: '화학분류', active: false},
      {title: '식약허가', active: false},
      {title: '치료', active: false}
    ]
  },
  {
    title: 'K-모듈',
    submenu: [
      {title: '논문 동향', active: false},
      {title: '시장 동향', active: false},
      {title: '연도별 모델 동향', active: false},
      {title: '연도별 시장 동향', active: false},
      {title: '연도별 오픈 데이터', active: false},
      {title: '사회이슈동향', active: false}
    ]
  },
  {
    title: '보유정보',
    submenu: [
      {title: '지식재산', active: false},
      {title: 'IPM 센터', active: false},
      {title: '기술이전', active: false},
      {title: '공용장비', active: false},
      {title: '협동연구', active: false},
      {title: '위탁사업체', active: false}
    ]
  },
  {
    title: '지원사업정보',
    submenu: [
      {title: '지원사업 공고', active: false},
      {title: '지원사업 신청안내', active: false},
      {title: '지원사업 동향', active: false},
      {title: '융자공간', active: false}
    ]
  },
  {
    title: '알림마당',
    submenu: [
      {title: '융자사업', active: false},
      {title: '특구뉴스', active: false},
      {title: '자료실', active: false},
      {title: '기업융복', active: false},
      {title: '산학협력 코너시스', active: false},
      {title: '홍보혁신융업', active: false},
      {title: '혁신창업자료', active: false},
      {title: '육성정보 산업', active: false}
    ]
  },
  {
    title: '특구소개',
    submenu: [
      {title: '멘토링', active: false},
      {title: '조직도', active: false},
      {title: '오시는길', active: false},
      {title: '홍보영상', active: false}
    ]
  },
  {
    title: '설문조사',
    submenu: [
      {title: '설문안내', active: false},
      {title: '공지사항자료', active: false},
      {title: '특구뉴스/기관홍보 자료', active: false},
      {title: '자료실안내', active: false},
      {title: '배너관리', active: false},
      {title: '팝업 관리', active: false},
      {title: '배너 및 관련안내', active: false},
      {title: 'SMS관리', active: false},
      {title: '로그확인기록', active: false},
      {title: '공통코드관리', active: false},
      {title: '위치적 관리', active: false}
    ]
  },
  {
    title: '관리자메뉴',
    submenu: [
      {title: '관리자메뉴', active: false}
    ]
  },
]);

const activateMenu = (index) => {
  activeMenuIndex.value = index;
  isAnyMenuActive.value = true;
};

const deactivateMenu = () => {
  activeMenuIndex.value = null;
  isAnyMenuActive.value = false;
};

</script>

<template>
  <div class="navbar-container">
    <nav class="navbar">
      <div class="navbar-logo">
        <img src="http://localhost:8080/img/logo.7b9102af.svg" alt="logo"/>
      </div>

      <div class="navbar-menu">
        <div
          v-for="(item, index) in menuItems"
          :key="index"
          class="menu-item"
          @mouseenter="activateMenu(index)"
          @mouseleave="deactivateMenu"
        >
          <a href="#" class="menu-link">{{ item.title }}</a>
        </div>
      </div>

      <div class="mega-menu-container" v-show="isAnyMenuActive">
        <div class="mega-menu-wrapper">
          <div class="mega-menu-image">
            <img src="http://localhost:8080/img/logo.7b9102af.svg" alt="Menu background" class="submenu-bg-image"/>
          </div>

          <div class="mega-menu-lists">
            <div
              v-for="(item, index) in menuItems"
              :key="index"
              class="menu-list-column"
              :class="{ 'active-column': activeMenuIndex === index }"
            >
              <ul class="submenu-list">
                <li
                  v-for="(subItem, subIndex) in item.submenu"
                  :key="subIndex"
                  class="submenu-item"
                  :class="{ 'active': subItem.active }"
                >
                  <a href="#" class="submenu-link">{{ subItem.title }}</a>
                </li>
              </ul>
            </div>
          </div>
          <div class="mega-menu-image">
            <img src="http://localhost:8080/img/logo.7b9102af.svg" alt="Menu background" class="submenu-bg-image"/>
          </div>

        </div>
      </div>

      <div class="navbar-buttons">
        <a href="#" class="icon-button">
          <span class="icon search-icon"></span>
        </a>
        <a href="#" class="icon-button">
          <span class="icon user-icon"></span>
        </a>
      </div>
    </nav>


  </div>
</template>

<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.navbar-container {
  width: 100%;
  border-bottom: 1px solid #eaeaea;
  background-color: #fff;
  position: relative;
  margin: 0 auto;
}

.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  max-width: 1450px;
  margin: 0 auto;
  padding: 0 20px;
  height: 70px;
}

.navbar-logo {
  flex: 0 0 auto;
}

.navbar-logo img {
  height: 40px;
  width: auto;
}

.navbar-menu {
  display: flex;
  font-weight: bold;
  width: 100%;
  cursor: pointer;
}

.menu-item {
  padding: 15px;
  position: relative;
  height: 100%;
  display: flex;
  align-items: center;
}

.menu-link {
  padding: 0 16px;
  height: 100%;
  display: flex;
  align-items: center;
  color: #333;
  text-decoration: none;
  font-size: 15px;
  transition: color 0.2s;
}

.menu-link:hover {
  color: #1e67a8;
}

/* Mega Menu */
.mega-menu-container {
  position: absolute;
  top: 100%;
  width: 100%;
  z-index: 100;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
  background-color: #fff;

}

.mega-menu-wrapper {
  display: flex;
  width: 100%;
}

.mega-menu-image {
  flex: 0 0 300px;
  background-color: #e9f5fb;
  padding: 24px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.submenu-bg-image {
  max-width: 100%;
  height: auto;
}

.mega-menu-lists {
  flex: 1;
  display: flex;
  flex-wrap: wrap;
  padding: 24px 0;
  justify-content: center;
}

.menu-list-column {
  display: block;
  padding: 0 16px;
  opacity: 0.7;
  transition: opacity 0.3s, background-color 0.3s;
}

.active-column {
  opacity: 1;
  background-color: #14274d;
}

.active-column .menu-category,
.active-column .submenu-link {
  color: #fff;
}

.menu-category {
  font-size: 16px;
  margin-bottom: 12px;
  color: #333;
  transition: color 0.3s;
  text-align: center;
}

.submenu-list {
  text-align: center;
  list-style: none;
}

.submenu-item {
  margin-bottom: 6px;
}

.submenu-link {
  display: block;
  padding: 8px 0;
  color: #555;
  text-decoration: none;
  font-size: 14px;
  transition: color 0.3s;
}

.active-column .submenu-item.active .submenu-link {
  font-weight: bold;
  color: #fff;
}

.navbar-buttons {
  display: flex;
  align-items: center;
}

.icon-button {
  width: 40px;
  height: 40px;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-left: 4px;
  border-radius: 50%;
  transition: background-color 0.2s;
}

.icon-button:hover {
  background-color: #f5f5f5;
}

.icon {
  width: 20px;
  height: 20px;
  background-position: center;
  background-repeat: no-repeat;
  background-size: contain;
}

.search-icon {
  background-image: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><circle cx="11" cy="11" r="8"></circle><line x1="21" y1="21" x2="16.65" y2="16.65"></line></svg>');
}

.user-icon {
  background-image: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M20 21v-2a4 4 0 0 0-4-4H8a4 4 0 0 0-4 4v2"></path><circle cx="12" cy="7" r="4"></circle></svg>');
}

</style>
