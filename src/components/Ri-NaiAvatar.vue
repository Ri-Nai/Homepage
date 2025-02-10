<script setup lang="ts">
import { defineProps } from 'vue'

defineProps<{ imageUrl: string | null }>()
</script>

<template>
  <img v-if="imageUrl" :src="imageUrl" alt="Ri-Nai Avatar" class="avatar" />

</template>


<style scoped>
.avatar {
  width: 100px;
  height: 100px;
  border-radius: 50%;
  border: 2px solid #fff;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);

  transition: cubic-bezier(0.215, 0.61, 0.355, 1);
  transition-duration: 3s;

  user-select: none;
  -webkit-user-select: none;
}

.avatar:hover {
  filter: drop-shadow(0 0 4em #646cffaa);
}
</style>
