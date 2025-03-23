<script setup>
import axios from 'axios'
import JobListing from './JobListing.vue'
import { reactive, defineProps, onMounted } from 'vue'
import PulseLoader from 'vue-spinner/src/PulseLoader.vue'

const state = reactive({
    jobs: [],
    isLoading: true
})

defineProps({
    limit: {
        type: Number,
    },
    showAllButton: {
        type: Boolean,
        default: false
    }
})

onMounted(async () => {
    try {
        const response = await axios.get('/api/jobs')
        state.jobs = response.data
    } catch (error) {
        console.error('Error fetching jobs: ' + error)
    } finally {
        setTimeout(() => {
            state.isLoading = false
        }, 1000)
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
        <!-- Loader -->
         <div v-if="state.isLoading" class="text-center text-gray-500 py-6">
            <PulseLoader />
         </div>
        <div v-else class="grid grid-cols-1 md:grid-cols-3 gap-6">
            <JobListing v-for="job in state.jobs.slice(0, limit || state.jobs.length)" :key="job.id" :job="job" />
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