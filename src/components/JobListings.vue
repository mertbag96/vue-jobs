<script setup>
import data from '@/jobs.json'
import { ref, defineProps } from 'vue'
import JobListing from './JobListing.vue'

const jobs = ref(data)

defineProps({
    limit: {
        type: Number,
        default: 6
    },
    showAllButton: {
        type: Boolean,
        default: false
    }
})
</script>

<template>
    <!-- Job Listings -->
    <section class="bg-green-50 px-4 py-10">
      <div class="container-xl lg:container m-auto">
        <h2 class="text-3xl font-bold text-green-500 mb-6 text-center">
          Browse Jobs
        </h2>
        <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
            <JobListing v-for="job in jobs.slice(0, limit || jobs.length)" :key="job.id" :job="job" />
        </div>
      </div>
    </section>

    <!-- View All Jobs -->
    <section 
        v-if="showAllButton" 
        class="m-auto max-w-lg my-10 px-6"
    >
        <a href="/jobs" class="block bg-black text-white text-center py-4 px-6 rounded-xl hover:bg-black/85">
            View All Jobs
        </a>
    </section>
</template>