<script setup>
import { defineProps } from 'vue'

defineProps({
    bg: String,
    default: 'bg-gray-100'
})
</script>

<template>
    <div :class="[bg, 'p-6 rounded-lg border shadow-md']">
        <slot></slot>
    </div>
</template>