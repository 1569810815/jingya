<template>
  <nav class="navbar">
    <RouterLink to="/" class="logo">
      <img src="#" alt="网站Logo" />
    </RouterLink>
    <ul class="nav-list">
      <li
        v-for="(item, index) in navItems"
        :key="index"
        class="nav-item"
        :class="{ 'has-dropdown': item.children }"
        @mouseenter="openIndex = index"
        @mouseleave="openIndex = null"
      >
        <RouterLink :to="item.src" class="nav-link">
          {{ item.Name }}
        </RouterLink>
        <ul
          v-if="item.children"
          class="dropdown-menu"
          v-show="openIndex === index"
        >
          <li v-for="child in item.children" :key="child.src">
            <RouterLink
              :to="child.src"
              class="dropdown-link"
              @click="closeDropdown"
            >
              {{ child.Name }}
            </RouterLink>
          </li>
        </ul>
      </li>
    </ul>
  </nav>
</template>

<script setup>
import { ref } from "vue";
import { RouterLink } from "vue-router";

const openIndex = ref(null);

const closeDropdown = () => {
  openIndex.value = null;
};

const navItems = ref([
  { Name: "首页", src: "/" },
  {
    Name: "产品简介",
    src: "/system",
    children: [
      { Name: "养老机构智慧管理系统", src: "/system" },
      { Name: "社区居家养老服务系统", src: "/community" },
      { Name: "养老公寓智慧管理系统", src: "/apartment" },
      { Name: "旅居养老服务系统", src: "/sojourning" },
      { Name: "智能硬件支持", src: "/device" },
    ],
  },
  { Name: "客户案例", src: "/case" },
  {
    Name: "新闻中心",
    src: "/news",
    children: [
      { Name: "新闻资讯", src: "/information" },
      { Name: "行业动态", src: "/dynamic" },
    ],
  },
  {
    Name: "关于我们", src: "/about"
  },
  {
    Name: "登录",
    src: "/individualLogin",
    children: [
      { Name: "个人登录", src: "/individualLogin" },
      { Name: "企业登录", src: "/enterpriseLogin" },
    ],
  },
]);
</script>

<style scoped>
.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 8vw;
  background-color: #fff;
  position: fixed;
  top: 0;
  right: 0;
  width: 100vw;
  height: 5rem;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.07);
  z-index: 1000;
}

.logo img {
  width: 7rem;
  height: 5rem;
  object-fit: contain;
  background-color: skyblue; /* 占位，实际使用时可移除 */
  margin-left: 0;
}

.nav-list {
  display: flex;
  list-style: none;
  margin: 0;
  padding: 0;
}

.nav-item {
  position: relative;
  margin: 0 2vw;
}

.nav-link {
  text-decoration: none;
  color: #222;
  font-size: 1.25rem;
  font-weight: 500;
  padding: 0.8rem 0;
  position: relative;
  transition: color 0.3s;
  background: none;
}

.nav-link:hover,
.nav-link:focus,
.nav-link.active {
  color: #05943c;
}

.nav-link:active {
  color: #e63946;
}

.nav-link:focus {
  outline: none;
}

.nav-link::after {
  content: "";
  position: absolute;
  left: 0;
  bottom: 0;
  width: 100%;
  height: 2px;
  background-color: #05943c;
  transform: scaleX(0);
  transition: transform 0.3s;
  transform-origin: right;
}

.nav-link:hover::after,
.nav-link:focus::after,
.nav-link.active::after {
  transform: scaleX(1);
  transform-origin: left;
}

.has-dropdown:hover .dropdown-menu,
.has-dropdown:focus-within .dropdown-menu {
  display: block;
}

.dropdown-menu {
  display: none;
  position: absolute;
  top: 100%;
  left: 0;
  min-width: 160px;
  background: #fff;
  box-shadow: 0 4px 16px rgba(0,0,0,0.10);
  border-radius: 6px;
  z-index: 1001;
  padding: 8px 0;
}

.dropdown-link {
  display: block;
  padding: 12px 32px;
  color: #333;
  text-decoration: none;
  font-size: 1rem;
  white-space: nowrap;
  transition: background 0.2s, color 0.2s;
  border-radius: 4px;
}

.dropdown-link:hover {
  background: #f5f5f5;
  color: #05943c;
}
</style>
