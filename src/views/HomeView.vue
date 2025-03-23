<script setup>
import Hero from '@/components/Hero.vue'
import HomeCards from '@/components/HomeCards.vue'
import JobListings from '@/components/JobListings.vue'
</script>

<template>
    <!-- Hero -->
    <Hero />

    <!-- Developers and Employers -->
    <HomeCards />

    <!-- Job Listings -->
    <JobListings limit="6" showAllButton="true" />
</template>