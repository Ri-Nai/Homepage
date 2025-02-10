<script setup lang="ts">

import { defineProps, ref, toRef, onMounted } from 'vue'

const props = defineProps<{
    imageUrl: string | null
    title: string | null
    url: string | null
}>()

const svgContent = ref<string | null>(null)

onMounted(async () => {
    if (props.imageUrl?.endsWith('.svg')) {
        const response = await fetch(props.imageUrl)
        svgContent.value = await response.text()
    }
})

</script>

<template>
    <div class="menu-button">
        <a v-if="url" :href="url">
            <template v-if="!imageUrl?.includes('null')">
                <div v-if="imageUrl?.endsWith('.svg')" class="menu-button-icon" v-html="svgContent" />
                <div v-else class="menu-button-icon">
                    <img :src="imageUrl" alt="icon" />
                </div>
            </template>
            <!-- <img v-else-if="imageUrl" class="menu-button-icon" :src="imageUrl" alt="icon" /> -->
            <span class="menu-button-title">{{ title }}</span>
        </a>
    </div>
</template>

<style scoped>
.menu-button {
    display: flex;
    align-items: center;
    justify-content: center;
    margin: 0.5em;
    padding: 0.5em;
    border-radius: 0.5em;
    background-color: rgba(255, 255, 255, 0.1);
    backdrop-filter: blur(10px);
    transition: background-color 0.3s;

    a {
        width: 7em;
        display: flex;
        align-items: center;
        justify-content: flex-start;
        text-decoration: none;

        .menu-button-title {
            flex: 1;
            text-align: center;
            /* margin-left: 0.5em; */
            font-size: 1.2em;
            font-weight: bold;
        }
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

svg {
    width: 100%;
    height: 100%;
}
</style>
