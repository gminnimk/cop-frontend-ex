<script setup>
import {ref, onMounted, onUnmounted} from 'vue';
import AppHeader from "@/components/AppHeader.vue";

// 공지사항 데이터
const notices = ref([
  {title: '관리자 공지사항 등록 테스트', hasButton: true},
  {title: '강원춘천 강소연구 개발특구에서는 독', hasButton: true},
  {title: '2023학년도 신입생 예비학기제 운영 안', hasButton: true},
  {title: '[강원지역혁신플랫폼 대학교육혁신본부] ', hasButton: true},
  {title: 'asdfasdf', hasButton: false}
]);

// 지원사업 데이터
const supportPrograms = ref([
  {title: '[공고] 강원춘천 강소연구개발특구 입주기업 모집'},
  {title: '[공고] 강원춘천 강소연구개발특구 입주기업 모집'}
]);

// 캐러셀 데이터
const carouselSlides = ref([
  {image: 'http://localhost:8080/img/home_bg2.0745c059.webp', alt: '강원 춘천 강소연구개발특구'},
  {
    image: 'data:image/jpeg;base64,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',
    alt: '강원 춘천 강소연구개발특구'
  },
  {
    image: 'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSJASGELh6r8Ix0iC3inqCsWaR-P3o9rX7aRw&s',
    alt: '강원 춘천 강소연구개발특구'
  }
]);

// 현재 슬라이드
const currentSlide = ref(0);
const currentSection = ref('main'); // Add this to track current section

// 아이콘 메뉴 데이터
const menuItems = ref([
  {title: '중소벤처24', icon: 'http://localhost:8080/img/navi1.4939cff2.svg'},
  {title: 'K-스타트업', icon: 'http://localhost:8080/img/navi2.b0018c11.svg'},
  {title: '중소기업혁명보시스템', icon: 'http://localhost:8080/img/navi3.88f14a15.svg'},
  {title: '기업마당', icon: 'http://localhost:8080/img/navi4.a9a510d6.svg'},
  {title: '소상공마당', icon: 'http://localhost:8080/img/navi5.e289d570.svg'},
  {title: '공공구매종합정보', icon: 'http://localhost:8080/img/navi6.92301192.svg'},
  {title: '강원지역혁신플랫폼\nGDV통합정보시스템', icon: 'http://localhost:8080/img/navi7.c1f85df6.svg'}
]);

// 슬라이드 이동 함수
const nextSlide = () => {
  currentSlide.value = (currentSlide.value + 1) % carouselSlides.value.length;
}

const prevSlide = () => {
  currentSlide.value = (currentSlide.value - 1 + carouselSlides.value.length) % carouselSlides.value.length;
}

// 섹션 이동 함수
const scrollToSection = (section) => {
  const element = document.getElementById(section);
  if (element) {
    element.scrollIntoView({behavior: 'smooth'});
    currentSection.value = section;
  }
}

// 스크롤 이벤트 핸들러
const handleWheel = (event) => {
  event.preventDefault();
  const sections = ['main', 'news'];
  const currentIndex = sections.indexOf(currentSection.value);

  if (event.deltaY > 0 && currentIndex < sections.length - 1) {
    // Scrolling down
    scrollToSection(sections[currentIndex + 1]);
  } else if (event.deltaY < 0 && currentIndex > 0) {
    // Scrolling up
    scrollToSection(sections[currentIndex - 1]);
  }
}

// 자동 슬라이드 기능
let slideInterval;

onMounted(() => {
  slideInterval = setInterval(() => {
    nextSlide();
  }, 5000);

  // Add wheel event listener
  window.addEventListener('wheel', handleWheel, {passive: false});
});

onUnmounted(() => {
  // Clean up
  clearInterval(slideInterval);
  window.removeEventListener('wheel', handleWheel);
});
</script>

<template>
  <div class="page-container">
    <div class="sections-container">
      <!-- Main Section -->
      <div id="main" class="main-container">
        <!-- 배경 이미지와 오버레이 -->
        <div class="background-overlay">
          <div class="main-content">
            <!-- 헤더 텍스트 -->
            <div class="header-text">
              <h1>
                강원춘천강소특구는 미래 지향적인 기업과 함께 혁신적인 사업 발전을 이루어 나가고, 지역 경제의 성장과 발전에 기여합니다
              </h1>
            </div>

            <!-- 중앙 컨텐츠 영역 -->
            <div class="center-content">
              <div class="center-content-all">
                <div class="center-content-head">
                  <!-- 공지사항 -->
                  <div class="content-box">
                    <div class="box-header">
                      <h2>공지사항</h2>
                      <button class="add-button">+</button>
                    </div>
                    <ul class="content-list">
                      <li v-for="(notice, index) in notices" :key="`notice-${index}`">
                        <span>{{ notice.title }}</span>
                        <button v-if="notice.hasButton" class="view-button">공고</button>
                      </li>
                    </ul>
                  </div>

                  <!-- 지원사업 -->
                  <div class="content-box">
                    <div class="box-header">
                      <h2>지원사업</h2>
                      <button class="add-button">+</button>
                    </div>
                    <ul class="content-list">
                      <li v-for="(support, index) in supportPrograms" :key="`support-${index}`">
                        <span>{{ support.title }}</span>
                      </li>
                    </ul>
                  </div>

                  <!-- 캐러셀 -->
                  <div class="carousel-container">
                    <div class="carousel-content">
                      <div class="carousel-slide" v-for="(slide, index) in carouselSlides" :key="`slide-${index}`"
                           :class="{ active: currentSlide === index }"
                      >
                        <img :src="slide.image" :alt="slide.alt">
                      </div>
                      <div class="carousel-pagination">
                        <span>{{ currentSlide + 1 }} / {{ carouselSlides.length }}</span>
                        <div class="carousel-controls">
                          <button @click="prevSlide">◀</button>
                          <button @click="nextSlide">▶</button>
                        </div>
                      </div>
                    </div>
                  </div>
                </div>
                <!-- 아이콘 메뉴 -->
                <div class="icon-menu">
                  <div class="icon-item" v-for="(item, index) in menuItems" :key="`menu-${index}`">
                    <div class="icon-box">
                      <img :src="item.icon" :alt="item.title">
                    </div>
                    <p class="multi-line">{{ item.title }}</p>
                  </div>
                </div>
              </div>

            </div>
          </div>
        </div>
      </div>

      <!-- 섹션 2 -->
      <div id="news" class="main-container">
        <div class="background-overlay-2">
          <div class="main-content">
            <div class="header-text">
              <h1>기업하기 좋은 특구, 기업과 함께하는 특구, 강원춘천강소특구</h1>
            </div>
            <div class="center-content">
              <div class="center-content-all">
                <div class="news-content">
                  <h2>Latest News</h2>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- 네비게이션 도트 메뉴 -->
      <div class="dot-navigation">
        <div class="dot-item" :class="{ active: currentSection === 'main' }" @click="scrollToSection('main')">
          <div class="dot"></div>
          <span>Main</span>
        </div>
        <div class="dot-connector"></div>
        <div class="dot-item" :class="{ active: currentSection === 'news' }" @click="scrollToSection('news')">
          <div class="dot"></div>
          <span>News</span>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
@import '@/styles/index.css';
</style>
