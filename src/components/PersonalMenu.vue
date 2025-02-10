<script setup lang="ts">

import { defineProps } from 'vue'

defineProps<{
    items: {
        title: string | null;
        url: string | null;
        icon: string | null;
    }[]
}>()


import MenuButton from './MenuButton.vue'



</script>

<template>
    <div class="personal-menu">
        <MenuButton v-for="(item, index) in items" 
            :key="index"
            :title="item.title"
            :url="item.url"
            :imageUrl="item.icon"
        />
    </div>
</template>

<style scoped>
.personal-menu {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    gap: 1em;
    margin-top: 2em;
}
</style>
