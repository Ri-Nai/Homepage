<script setup lang="ts">

import { defineProps, ref, onMounted } from 'vue'

const props = defineProps<{
  imageUrl: string | null
  title: string | null
  url: string | null
}>()

const svgContent = ref<string | null>(null)

onMounted(async () => {
  if (props.imageUrl?.includes('svg')) {
    const response = await fetch(props.imageUrl)
    svgContent.value = await response.text()
  }
})

</script>

<template>
  <a :href="url || ''" :title="title || ''">
    <div class="menu-button">
      <template v-if="!imageUrl?.includes('null')">
        <div v-if="imageUrl?.includes('svg')" class="menu-button-icon" v-html="svgContent" />
        <div v-else class="menu-button-icon">
          <img :src="imageUrl || ''" alt="icon" />
        </div>
      </template>
      <span class="menu-button-title">{{ title }}</span>
    </div>
  </a>
</template>

<style scoped>
.menu-button {
  display: flex;
  align-items: center;
  justify-content: flex-start;
  width: 7em;
  margin: 0.5em;
  padding: 0.5em;
  border-radius: 0.5em;
  background-color: rgba(255, 255, 255, 0.1);
  box-shadow: 0 0 10px rgba(255, 255, 255, 0.2);
  backdrop-filter: blur(10px);
  transition: 0.6s cubic-bezier(0.25, 0.8, 0.25, 1);

  text-decoration: none;

  .menu-button-title {
    flex: 1;
    text-align: center;
    /* margin-left: 0.5em; */
    font-size: 1.2em;
    font-weight: bold;
    user-select: none;
    -webkit-user-select: none;
  }

}



.menu-button:hover {
  background-color: rgba(255, 255, 255, 0.2);
}

.menu-button-icon {
  width: 2em;
  height: 2em;
  margin-right: 0.5em;

}


@media (prefers-color-scheme: light) {
  .menu-button {
    background-color: rgba(0, 0, 0, 0.1);
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.4);

  }

  .menu-button:hover {
    background-color: rgba(0, 0, 0, 0.2);
  }
}
</style>
