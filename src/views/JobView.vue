<script setup>
import axios from 'axios'
import { reactive, onMounted } from 'vue'
import { useRoute, RouterLink, useRouter } from 'vue-router'
import BackButton from '@/components/BackButton.vue'
import PulseLoader from 'vue-spinner/src/PulseLoader.vue'
import { useToast } from 'vue-toastification'

const toast = useToast()

const route = useRoute()
const router = useRouter()

const jobId = route.params.id

const state = reactive({
    job: {},
    isLoading: true
})

const deleteJob = async () => {
    try {
        const confirm = window.confirm('Are you sure you want to delete this job?')

        if (confirm) {
            await axios.delete('/api/jobs/' + jobId)
            toast.success('Job deleted successfully!')
            router.push('/jobs')
        } else {
            toast.error('Job deletion canceled.')
        }
    } catch (error) {
        toast.error('Job could not be deleted. Please try again.')
        console.error('Error deleting job: ' + error)
    }
}   

onMounted(async () => {
    try {
        const response = await axios.get('/api/jobs/' + jobId)
        state.job = response.data
    } catch (error) {
        console.error('Error fetching job: ' + error)
    } finally {
        setTimeout(() => {
            state.isLoading = false
        }, 1000)
    }
})
</script>

<template>
    <BackButton />
    <section v-if="!state.isLoading" class="bg-green-50">
        <div class="container m-auto py-10 px-6">
            <div class="grid grid-cols-1 md:grid-cols-70/30 w-full gap-6">
                <!-- Main -->
                <main>
                    <div class="bg-white p-6 rounded-lg shadow-md text-center md:text-left">
                        <div class="text-gray-500 mb-4">
                            {{ state.job.type }}
                        </div>

                        <h1 class="text-3xl font-bold mb-4">
                            {{ state.job.title }}
                        </h1>

                        <div class="text-gray-500 font-semibold mb-4 flex align-middle justify-center md:justify-start">
                            <div class="flex items-center space-x-2">
                                <i class="pi pi-map-marker text-orange-700"></i>
                                <p class="text-orange-700">
                                    {{ state.job.location }}
                                </p>
                            </div>
                        </div>
                    </div>
                    
                    <div class="bg-white p-6 rounded-lg shadow-md mt-6">
                        <h3 class="text-green-800 text-lg font-bold mb-6">
                            Job Description
                        </h3>
                        <p class="mb-4">
                            {{ state.job.description }}
                        </p>
                        
                        <h3 class="text-green-800 text-lg font-bold mb-2">
                            Salary
                        </h3>
                        <p class="mb-4">
                            {{ state.job.salary }}
                        </p>
                    </div>
                </main>
                
                <!-- Aside -->
                <aside>
                    <!-- Company Info -->
                     <div class="bg-white p-6 rounded-lg shadow-md">
                        <h3 class="text-xl font-bold mb-6">
                            Company Info
                        </h3>

                        <h2 class="text-2xl">
                            {{ state.job.company.name }}
                        </h2>

                        <p class="my-2">
                            {{ state.job.company.description }}
                        </p>

                        <hr class="my-4" />

                        <h3 class="text-xl">Contact Email:</h3>

                        <p class="my-2 bg-green-100 p-2 font-bold">
                            {{ state.job.company.contactEmail }}
                        </p>

                        <h3 class="text-xl">Contact Phone:</h3>

                        <p class="my-2 bg-green-100 p-2 font-bold">
                            {{ state.job.company.contactPhone }}
                        </p>
                    </div>

                    <!-- Manage Job -->
                    <div class="bg-white p-6 rounded-lg shadow-md mt-6">
                        <h3 class="text-xl font-bold mb-6">Manage Job</h3>

                        <!-- Edit Job -->
                        <RouterLink 
                            :to="`/jobs/edit/${state.job.id}`"
                            class="bg-green-500 hover:bg-green-600 text-white text-center font-bold py-2 px-4 rounded-full w-full focus:outline-none focus:shadow-outline mt-4 block"
                        >Edit Job
                        </RouterLink>

                        <!-- Delete Job -->
                        <button
                            @click="deleteJob" 
                            class="bg-red-500 hover:bg-red-600 text-white font-bold py-2 px-4 rounded-full w-full focus:outline-none focus:shadow-outline mt-4 block">
                            Delete Job
                        </button>
                    </div>
                </aside>
            </div>
        </div>
    </section>
    <!-- Loader -->
    <div v-else class="text-center text-gray-500 py-12">
        <PulseLoader />
    </div>
</template>