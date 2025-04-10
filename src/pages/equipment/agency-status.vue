<script setup>
import {ref, onMounted, computed} from 'vue';
import SideBar from '@/components/SideBar.vue';

const centers = ref([
  {
    name: '친환경농업연구센터',
    equipmentCount: 103,
    address: '강원특별자치도 춘천시 강원대학길 1, 대학교 3층',
    phone: '033-250-1103',
    website: 'https://www.center.com/centercenter',
    image: '/images/center1.jpg'
  },
  {
    name: '공동실험실습관',
    equipmentCount: 103,
    address: '강원특별자치도 춘천시 강원대학길 1, 대학교 3층',
    phone: '033-250-1103',
    website: 'https://www.center.com/centercenter',
    image: '/images/center2.jpg'
  },
  {
    name: '공동실험실습관',
    equipmentCount: 103,
    address: '강원특별자치도 춘천시 강원대학길 1, 대학교 3층',
    phone: '033-250-1103',
    website: 'https://www.center.com/centercenter',
    image: '/images/center3.jpg'
  },
  {
    name: '공동실험실습관',
    equipmentCount: 103,
    address: '강원특별자치도 춘천시 강원대학길 1, 대학교 3층',
    phone: '033-250-1103',
    website: 'https://www.center.com/centercenter',
    image: '/images/center4.jpg'
  }
]);

const centersArray = computed(() => centers.value);
const totalEquipment = 2050;
const searchText = ref('');
const isLoading = ref(true);

onMounted(() => {
  setTimeout(() => {
    isLoading.value = false;
  }, 800);
});

const searchEquipment = () => {
  console.log('검색어:', searchText.value);
};
</script>

<template>
  <div class="page-layout">
    <div class="main-content">
      <div class="sidebar-container">
        <SideBar/>
      </div>
      <div class="agency-content">
        <div class="agency-status-container">
          <div class="breadcrumb">
            <span><img src="" alt="홈" class="home-icon"></span>
            <span class="separator">></span>
            <span>보유정보</span>
            <span class="separator">></span>
            <span class="current">기관별 현황</span>
          </div>

          <h1 class="page-title">기관별 현황</h1>

          <div v-if="isLoading" class="loading-container">
            <div class="loading-spinner"></div>
            <p>데이터를 불러오는 중입니다...</p>
          </div>

          <div v-else>
            <div class="summary-box">
              <div class="equipment-count">
                <p>장비현황 전체 보유장비</p>
                <p class="count">{{ totalEquipment }}대</p>
              </div>
            </div>

            <div class="search-box">
              <input type="text" v-model="searchText" placeholder="검색어를 입력해주세요." class="search-input">
              <button @click="searchEquipment" class="search-btn">검색</button>
            </div>

            <div class="centers-title">
              <span>전체 {{ centersArray.length }}개</span>
            </div>

            <div class="centers-grid">
              <div v-for="(c, i) in centersArray" :key="i" class="center-card">
                <div class="center-image">
                  <img src="" alt="건물 이미지">
                </div>
                <div class="center-detail">
                  <h3 class="center-name">{{ c.name }}</h3>
                  <div class="equipment-badge">{{ c.equipmentCount }}개 장비 보유</div>
                  <div class="center-content">
                    <p class="center-address">{{ c.address }}</p>
                    <p class="center-phone">{{ c.phone }}</p>
                    <p class="center-website">
                      <i class="home-icon"></i>
                      {{ c.website }}
                    </p>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
@import "@/styles/agency-status.css";
</style>
