<script setup>
import { RouterLink } from 'vue-router'
</script>

<template>
    <section>
        <div class="container m-auto py-6 px-6">
            <RouterLink 
                to="/jobs" 
                class="font-semibold text-green-600 hover:text-green-500 flex items-center space-x-2"
            >
                <i class="pi pi-arrow-left"></i>
                    <span>Back to Jobs</span>
            </RouterLink>
        </div>
    </section>
</template>