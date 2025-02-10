<script setup lang="ts">
import { ref } from 'vue'
import yaml from 'js-yaml'

import BackgroundImage from './components/BackgroundImage.vue'
import Ri_NaiAvatar from './components/Ri-NaiAvatar.vue'
import FadeIn from './components/FadeIn.vue'
import PersonalMenu from './components/PersonalMenu.vue'
// 使用 ?raw 后缀导入 config.yaml 的原始内容
import configText from './config.yaml?raw'

// 解析 YAML 得到配置对象
const config = yaml.load(configText)

// 定义 reactive 数据
const bgUrl = ref<string | null>()
bgUrl.value = new URL(config.background, import.meta.resolve('./')).href

const avatarUrl = ref<string | null>(config?.avatar || null)
avatarUrl.value = new URL(config.avatar, import.meta.resolve('./')).href


for (const item of config.menu) {
  item.icon = new URL(item.icon, import.meta.resolve('./')).href
}

console.log('config:', config)

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
