<script setup>
import { useSlots } from 'vue';

// 获取默认插槽中的所有子节点
const slots = useSlots();
const slotChildren = slots.default ? slots.default() : [];
</script>


<template>
    <div class="fade-in-container">
        <!-- 遍历默认插槽的所有 VNode，将每个节点包装在一个 div 中 -->
        <template v-for="(child, index) in slotChildren" :key="index">
            <div class="fade-in-child" :style="{ '--delay-index': index + 1 }">
                <component :is="child" />
            </div>
        </template>
    </div>
</template>

<style scoped>
/* 包装容器 */
.fade-in-container {
    /* 可根据需要调整布局 */
    display: flex;
    flex-direction: column;
    align-items: center;
}

/* 子元素初始状态和动画 */
.fade-in-child {
    opacity: 0;
    transform: translateY(30px);
    /* 初始位置向下偏移 */
    animation: slideIn 1s cubic-bezier(0.23, 1, 0.32, 1) forwards;
    /* 根据自定义属性计算动画延迟 */
    animation-delay: calc(var(--delay-index) * 0.2s - 0.2s);
}

/* 动画关键帧：从下向上淡入 */
@keyframes slideIn {
    from {
        opacity: 0;
        transform: translateY(30px);
    }

    to {
        opacity: 1;
        transform: translateY(0);
    }
}
</style>
