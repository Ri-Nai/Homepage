<script setup lang="ts">
import { ref } from 'vue'

// import config from './config'
import yaml from 'js-yaml'
import configText from './config.yaml?raw'

const config: any = yaml.load(configText)

// 定义 reactive 数据
// 使用 import.meta.glob 动态导入所有图片
const images: Record<string, { default: string }> = import.meta.glob(['./assets/*', './assets/icons/*'], { eager: true });

for (const path in images) {
  console.log(`Image path: ${path}`, images[path].default);
}

const bgUrl = ref<string | null>(null)
const avatarUrl = ref<string | null>(config?.avatar || null)

if (config.background) {
  config.background = images[config.background]?.default || '';
  bgUrl.value = config.background;
}

if (config.avatar) {
  config.avatar = images[config.avatar]?.default || '';
  avatarUrl.value = config.avatar;
}

for (const item of config.menu) {
  if (item.icon) {
    item.icon = images[item.icon]?.default || '';
  }
}


console.log('config:', config)

import BackgroundImage from './components/BackgroundImage.vue'
import Ri_NaiAvatar from './components/Ri-NaiAvatar.vue'
import FadeIn from './components/FadeIn.vue'
import PersonalMenu from './components/PersonalMenu.vue'
</script>

<template>
  <BackgroundImage :imageUrl="bgUrl" />
  <FadeIn>
    <Ri_NaiAvatar :imageUrl="avatarUrl" />
    <h2> Reina </h2>
    <h4 style="margin-top: 0em;"> 如果努力的尽头就是奇迹 </h4>
    <PersonalMenu :items="config.menu" />
  </FadeIn>
</template>


<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}

.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}

.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
