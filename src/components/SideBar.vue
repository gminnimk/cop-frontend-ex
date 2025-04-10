<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter();

const menus = ref([
  {
    name: "지식재산권",
    expanded: false,
    subMenus: []
  },
  {
    name: "공용장비",
    expanded: true,
    subMenus: ["기관별 현황", "전체 장비 목록", "산업혁단 장비 예약", "장비 예약관리(관리자)"]
  },
  {
    name: "입주공간",
    expanded: false,
    subMenus: []
  },
  {
    name: "회의실 예약",
    expanded: false,
    subMenus: []
  }
]);

const toggleMenu = (menu) => {
  menu.expanded = !menu.expanded;
}

const navigateTo = (subMenu) => {
  if (subMenu === "기관별 현황") {
    router.push('/equipment/agency-status');
  }
}
</script>

<template>
  <div class="side-container">
    <div class="side-container-title">
      <h1>보유정보</h1>
    </div>
    <div v-for="menu in menus" :key="menu.name" class="menu-item">
      <div class="menu-header" @click="toggleMenu(menu)">
        <span>{{ menu.name }}</span>
        <span class="toggle-icon">{{ menu.expanded ? '－' : '＋' }}</span>
      </div>
      <div v-if="menu.expanded" class="submenu">
        <div v-for="subMenu in menu.subMenus" :key="subMenu" class="submenu-item" @click="navigateTo(subMenu)">
          <span class="submenu-dash">－</span>
          <span>{{ subMenu }}</span>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.side-container {
  width: 250px;
  border: 1px solid #e0e0e0;
  font-family: 'Noto Sans KR', sans-serif;
}

.side-container-title {
  background-color: #153259;
  color: white;
  padding: 15px;
  margin: 0;
}

.side-container-title h1 {
  margin: 0;
  font-size: 18px;
  font-weight: 600;
}

.menu-item {
  border-bottom: 1px solid #e0e0e0;
}

.menu-header {
  display: flex;
  justify-content: space-between;
  padding: 12px 15px;
  cursor: pointer;
  align-items: center;
}

.toggle-icon {
  color: #153259;
  font-weight: bold;
  font-size: 18px;
}

.submenu {
  background-color: #f5f5f5;
}

.submenu-item {
  padding: 10px 15px 10px 25px;
  display: flex;
  align-items: center;
  font-size: 14px;
  cursor: pointer;
}

.submenu-item:hover {
  background-color: #e8e8e8;
}

.submenu-dash {
  color: #153259;
  margin-right: 8px;
}

.menu-header:hover {
  background-color: #f0f0f0;
}
</style>
