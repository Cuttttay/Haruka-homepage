<!-- App.vue -->
<template>
  <el-header class="header">
    <div class="nav-bg" ></div>
    <div class="nav">
      <div class="contain-center">
        <img
            src="../phot0/img_1.png"
            class="logo-img"
            alt="希望像鸟一样自由"
        >
        <el-menu
            mode="horizontal"
            class="nav-menu"
            :class="{ 'dark-menu': isDark }"
            default-active="1"
            active-text-color="#ff69b4"
            text-color="#333"
        >
          <el-menu-item index="1">个人主页</el-menu-item>
          <el-menu-item index="2" >影音书分享</el-menu-item>
          <el-menu-item index="3">编程心得</el-menu-item>
          <el-menu-item index="4">美食探寻</el-menu-item>
        </el-menu>
      </div>
      <el-switch
          v-model="isDark"
          inline-prompt
          :active-icon="Moon"
          :inactive-icon="Sunny"
          @change="toggleTheme"
      />
    </div>
  </el-header>

  <!-- 主要内容 -->
  <div class="main-container">
    <!-- 卡片 -->
    <div class="profile-vertical">
      <div
          class="full-bg"
          :style="{ backgroundImage: `url(${avatarUrl})` }"
      ></div>

      <div class="profile-content">
        <el-avatar
            :size="100"
            :style="{
          'background-color': 'transparent',
          'border': 'none'
        }"
            class="sidebar-avatar"
        />
      <h2 class="name">Sakura</h2>
      <p class="position">乘风好去，长空万里，直下看山河</p>
      </div>
      <el-divider class="divider"/>
      <div class="social-links-vertical">
        <el-link
            :icon="Link"
            href="#"
            class="social-btn"
            target="_blank"
            style="color:pink"
        >
          <span class="social-text">GitHub</span>
        </el-link>
        <el-link
            :icon="Link"
            href="#"
            class="social-btn"
            target="_blank"
            style="color:pink"
        >
          <span class="social-text">LinkedIn</span>
        </el-link>
      </div>
    </div>

    <!-- 详细信息标签页 -->
    <div class="content-section">
      <el-tabs
          type="border-card"
          tab-position="top"
          default-active="1"
          active-text-color="#ff69b4"
          text-color="#333"
      >
        <el-tab-pane text-color="#ff69b4"
            label="关于我">


          <p class="description">
            <ul>
              <li>兴趣爱好：读书、唱歌、运动、旅游、探店、看动漫</li>
              <li>专业：信息与计算科学</li>
              <li> 专注于现代Web技术栈，擅长：</li>
            </ul>
            </p>


          <el-space wrap>
            <el-tag type="success">Vue 3</el-tag>
            <el-tag type="warning">Node.js</el-tag>
            <el-tag type="danger">TypeScript</el-tag>
          </el-space>
        </el-tab-pane>

        <el-tab-pane label="项目经验">
          <el-timeline>
            <el-timeline-item
                v-for="(item, index) in projects"
                :key="index"
                :timestamp="item.time"
                placement="top"
            >
              <el-card>
                <h4>{{ item.title }}</h4>
                <p>{{ item.description }}</p>
              </el-card>
            </el-timeline-item>
          </el-timeline>
        </el-tab-pane>
      </el-tabs>
    </div>
  </div>
</template>


<script setup>
import { ref } from 'vue'
import { Moon, Sunny, Link } from '@element-plus/icons-vue'
/*
import {StartSakura} from'@/js/fullScreenFlower'
const isDark = ref(false)
*/

const avatarUrl = '../phot0/img_3.png'

const projects = [
  {
    time: '2025',
    title: '小小计算器',
    description: '基于kotlin的基本项目'
  },
  {
    time: '2025',
    title: '女性健康安全网站（筹备中）',
    description: '使用 vue 实现网页基本功能'
  }
]

const toggleTheme = () => {
  document.documentElement.classList.toggle('dark', isDark.value)
}
</script>

<style scoped>
.logo-img {
  height: 50px;
  margin-right: 30px;
  cursor: pointer;
  transition: opacity 0.3s;
}

.header {
  position: relative;
  overflow: hidden;
  background: transparent!important;
}
.nav-bg {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-size: cover;
  background-position: center;
  opacity: 0.9;
  z-index: 1;
}
.nav {
  display: flex;
  justify-content: space-between;
  align-items: center;
  height: 100%;
  position: relative;
  z-index: 2;
}

.nav-menu {
  ::v-deep .el-menu-item.is-active {
    border-bottom-color: #ff69b4 !important; /* 粉红色下划线 */
    border-bottom-width: 3px;
    transition: border-color 0.3s;
  }
}

/* 暗色主题样式 */
.dark-menu {
  background-color: #141414;
  text-color: #fff !important;
}

.dark-menu .el-menu-item {
  color: rgba(255, 255, 255, 0.9) !important;
}

.dark-menu .el-menu-item:hover {
  background-color: #262626 !important;
}
/* 新增样式 */
.profile-vertical {
  position: relative;
  border-radius: 12px; /* 圆角效果 */
  overflow: hidden;
}

.full-bg {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-size: cover;
  background-position: center;
  opacity: 0.8;
  z-index: 1;
}

.profile-content {
  position: relative;
  z-index: 2; /* 确保内容在前景 */
  padding: 2rem;
}
 .position, .introduce, .social-text {
  text-shadow: 0 1px 3px rgba(0, 0, 0, 0.3);
  text-align: center;
}
.name{
  font-size: 4rem;
  text-shadow: 0 1px 3px rgba(0, 0, 0, 0.3);
  text-align: center;
}
.dark .full-bg {
  opacity: 0.2;
}

.dark .name,
.dark .position,
.dark .introduce {
  color: #fff !important;
  text-shadow: 0 1px 3px rgba(0, 0, 0, 0.8);
}
.sidebar-avatar {
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
  margin-bottom: 1.5rem;
}

/* 暗色模式适配 */
.dark .profile-vertical {
  background: rgba(40, 40, 40, 0.85);
}


/* 精确控制背景高度 */

.contain-center{
  display: flex;
  align-items: center;
  max-width: 1200px; /* 控制最大宽度 */
  width: 100%;
  justify-content: center; /* 内容居中 */
}
.description {
  line-height: 1.8;
  color: var(--el-text-color-regular);
}
main.container {
  max-width: 1200px;
  margin: 20px auto;
  padding: 0 20px;
}

.content-section {
  background: transparent!important;
  box-shadow:none!important;
  border-radius:0!important;
}
/*标签页样式调整*/
:deep(.el-tab--card){
  border: none;
}

:deep(.el-tabs__nav-wrap){
  padding: 0 20px;
  background:#fff;
  border-radius: 8px 8px 0 0;
}
:deep(.el-tabs__item) {
  height: 48px;
  line-height: 48px;
}

/* 时间线优化 */
.el-timeline {
  padding: 20px;
}

/* 移动端适配 */
@media (max-width: 768px) {
  .profile-card {
    margin-bottom: 20px;
  }

  :deep(.el-tabs__nav-wrap) {
    overflow-x: auto;
  }
}
/* 垂直布局调整 */
.profile-vertical {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 1.5rem;
}

.sidebar-avatar {
  margin-bottom: 1.5rem;
  border: 3px solid var(--el-color-primary);
}


.name {
  margin: 0.8rem 0;
  font-size: 1rem;

}

.position {
  color: black;
  text-align: center;
  font-size: 1rem;
  margin-bottom: 1rem;
  justify-content: center;
}

/* 垂直分割线 */
.divider {
  width: 80%;
  margin: 1.2rem 0;
}

/* 垂直社交链接 */
.social-links-vertical {
  width: 100%;
  display: flex;
  flex-direction: column;
  gap: 0.8rem;
  z-index: 1;
}

.social-btn {
  display: flex;
  align-items: center;
  padding: 8px 15px;
  transition: all 0.3s;

  &:hover {
    background: lightpink;
    transform: translateX(5px);
  }
}

.social-text {
  margin-left: 8px;
  font-weight: 500;

}

</style>