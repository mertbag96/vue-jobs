<script setup>
import axios from 'axios'
import router from '@/router'
import { reactive, onMounted } from 'vue'
import { useToast } from 'vue-toastification'
import { useRoute } from 'vue-router'
import PulseLoader from 'vue-spinner/src/PulseLoader.vue'

const toast = useToast()

const route = useRoute()

const jobId = route.params.id

const form = reactive({
    type: 'Full-Time',
    title: '',
    description: '',
    salary: 'Under $50K',
    location: '',
    company: {
        name: '',
        description: '',
        contactEmail: '',
        contactPhone: ''
    }
})

const state = reactive({
    job: {},
    isLoading: true
})

const handleSubmit = async () => {
    try {
        const updatedJob = {
            type: form.type,
            title: form.title,
            description: form.description,
            salary: form.salary,
            location: form.location,
            company: {
                name: form.company.name,
                description: form.company.description,
                contactEmail: form.company.contactEmail,
                contactPhone: form.company.contactPhone
            }
        }
    
        const response = await axios.put(`/api/jobs/${jobId}`, updatedJob)

        toast.success('Job updated successfully!')

        router.push(`/jobs/${response.data.id}`)
    } catch (error) {

        toast.error('Job could not be updated. Please try again.')
        console.error('Error adding job: ' + error)
    }
}

onMounted(async () => {
    try {
        const response = await axios.get('/api/jobs/' + jobId)
        
        state.job = response.data

        form.type = state.job.type
        form.title = state.job.title
        form.description = state.job.description
        form.salary = state.job.salary
        form.location = state.job.location
        form.company.name = state.job.company.name
        form.company.description = state.job.company.description
        form.company.contactEmail = state.job.company.contactEmail
        form.company.contactPhone = state.job.company.contactPhone
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
    <section class="bg-green-50">
        <div class="container m-auto max-w-2xl py-24">
            <div class="bg-white px-6 py-8 mb-4 shadow-md rounded-md border m-4 md:m-0">
                <form @submit.prevent="handleSubmit">
                    <h2 class="text-3xl text-center font-semibold mb-6">Edit Job</h2>
                    
                    <div v-if="!state.isLoading">
                        <!-- Job Type -->
                        <div class="mb-4">
                            <label for="type" class="block text-gray-700 font-bold mb-2">
                                Job Type
                                <small class="font-semibold text-red-500">*</small>
                            </label>

                            <select 
                                id="type" 
                                name="type" 
                                class="border rounded w-full py-2 px-3" 
                                required
                                v-model="form.type"
                            >
                                <option value="Full-Time">Full-Time</option>
                                <option value="Part-Time">Part-Time</option>
                                <option value="Remote">Remote</option>
                                <option value="Internship">Internship</option>
                            </select>
                        </div>

                        <!-- Job Title -->
                        <div class="mb-4">
                            <label for="title" class="block text-gray-700 font-bold mb-2">
                                Job Title
                                <small class="font-semibold text-red-500">*</small>
                            </label>
                            
                            <input
                                type="text"
                                id="title"
                                name="title"
                                class="border rounded w-full py-2 px-3 mb-2"
                                placeholder="eg. Vue.js Developer"
                                required
                                v-model="form.title"
                            />
                        </div>

                        <!-- Job Description -->
                        <div class="mb-4">
                            <label for="description" class="block text-gray-700 font-bold mb-2">
                                Description
                                <small class="font-semibold text-red-500">*</small>
                            </label>
                            
                            <textarea
                                id="description"
                                name="description"
                                class="border rounded w-full py-2 px-3"
                                rows="4"
                                placeholder="Add any job duties, expectations, requirements, etc"
                                v-model="form.description"></textarea>
                        </div>

                        <!-- Job Salary -->
                        <div class="mb-4">
                            <label for="salary" class="block text-gray-700 font-bold mb-2">
                                Salary
                                <small class="font-semibold text-red-500">*</small>
                            </label>

                            <select
                                id="salary"
                                name="salary"
                                class="border rounded w-full py-2 px-3"
                                required
                                v-model="form.salary"
                            >
                                <option value="Under $50K">Under $50K</option>
                                <option value="$50K - $60K">$50 - $60K</option>
                                <option value="$60K - $70K">$60 - $70K</option>
                                <option value="$70K - $80K">$70 - $80K</option>
                                <option value="$80K - $90K">$80 - $90K</option>
                                <option value="$90K - $100K">$90 - $100K</option>
                                <option value="$100K - $125K">$100 - $125K</option>
                                <option value="$125K - $150K">$125 - $150K</option>
                                <option value="$150K - $175K">$150 - $175K</option>
                                <option value="$175K - $200K">$175 - $200K</option>
                                <option value="Over $200K">Over $200K</option>
                            </select>
                        </div>

                        <!-- Job Location -->
                        <div class="mb-4">
                            <label for="location" class="block text-gray-700 font-bold mb-2">
                                Location
                                <small class="font-semibold text-red-500">*</small>
                            </label>

                            <input
                                type="text"
                                id="location"
                                name="location"
                                class="border rounded w-full py-2 px-3 mb-2"
                                placeholder="Company Location"
                                required
                                v-model="form.location"
                            />
                        </div>

                        <h3 class="text-2xl mb-5">Company Info</h3>

                        <!-- Company Name -->
                        <div class="mb-4">
                            <label for="company_name" class="block text-gray-700 font-bold mb-2">
                                Name
                                <small class="font-semibold text-red-500">*</small>
                            </label>

                            <input
                                type="text"
                                id="company_name"
                                name="company_name"
                                class="border rounded w-full py-2 px-3"
                                placeholder="Company Name"
                                v-model="form.company.name"
                            />
                        </div>

                        <!-- Company Description -->
                        <div class="mb-4">
                            <label for="company_description" class="block text-gray-700 font-bold mb-2">
                                Description
                                <small class="font-semibold text-red-500">*</small>
                            </label>

                            <textarea
                                id="company_description"
                                name="company_description"
                                class="border rounded w-full py-2 px-3"
                                rows="4"
                                placeholder="What does your company do?"
                                v-model="form.company.description"></textarea>
                        </div>

                        <!-- Company Contact Email -->
                        <div class="mb-4">
                            <label for="contact_email" class="block text-gray-700 font-bold mb-2">
                                Contact Email
                                <small class="font-semibold text-red-500">*</small>
                            </label>

                            <input
                                type="email"
                                id="contact_email"
                                name="contact_email"
                                class="border rounded w-full py-2 px-3"
                                placeholder="Email address for applicants"
                                required
                                v-model="form.company.contactEmail"
                            />
                        </div>

                        <!-- Company Contact Phone -->
                        <div class="mb-4">
                            <label for="contact_phone" class="block text-gray-700 font-bold mb-2">
                                Contact Phone
                                <small class="font-semibold text-red-500">*</small>
                            </label>
                            
                            <input
                                type="tel"
                                id="contact_phone"
                                name="contact_phone"
                                class="border rounded w-full py-2 px-3"
                                placeholder="Optional phone for applicants"
                                v-model="form.company.contactPhone"
                            />
                        </div>

                        <!-- Submit Button -->
                        <div>
                            <button 
                                class="bg-green-500 hover:bg-green-600 text-white font-bold py-2 px-4 rounded-xl w-full focus:outline-none focus:shadow-outline" 
                                type="submit"
                            >Update Job
                            </button>
                        </div>
                    </div>
                    <!-- Loader -->
                    <div v-else class="text-center text-gray-500 py-12">
                        <PulseLoader />
                    </div>
                </form>
            </div>
        </div>
    </section>
</template>