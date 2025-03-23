<script setup>
import { RouterLink, useRoute } from 'vue-router'

const staticClasses = [
    'text-white', 
    'px-3', 
    'py-2', 
    'rounded-md'
]

const isActive = (routePath) => {
    const route = useRoute()
    return route.path === routePath
}
</script>

<template>
    <div class="md:ml-auto">
        <div class="flex space-x-2">
            <!-- Home -->
            <RouterLink 
                to="/" 
                :class="[
                    isActive('/') 
                    ? 'bg-green-900' 
                    : 'hover:bg-gray-900 hover:text-white', 
                    ...staticClasses
                ]"
            >Home</RouterLink>

            <!-- Jobs -->
            <RouterLink 
                to="/jobs" 
                :class="[
                    isActive('/jobs') 
                    ? 'bg-green-900' 
                    : 'hover:bg-gray-900 hover:text-white', 
                    ...staticClasses
                ]"
            >Jobs</RouterLink>

            <!-- Add Job -->
            <RouterLink 
                to="/add-job" 
                :class="[
                    isActive('/add-job') 
                    ? 'bg-green-900' 
                    : 'hover:bg-gray-900 hover:text-white', 
                    ...staticClasses
                ]"
            >Add Job</RouterLink>
        </div>
    </div>
</template>