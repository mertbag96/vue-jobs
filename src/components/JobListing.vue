<script setup>
import { defineProps, ref, computed } from 'vue'

const props = defineProps({
    job: Object
})

const showFullDescription = ref(false)

const toggleDescription = () => {
    showFullDescription.value = !showFullDescription.value
}

const truncatedDescription = computed(() => {
    let description = props.job.description
    if (!showFullDescription.value) {
        description = description.substring(0, 124) + '...'
    }

    return description
})
</script>

<template>
    <!-- Job Listing -->
    <div class="bg-white rounded-xl shadow-md relative">
        <div class="p-4">
            <div class="mb-6">
                <div class="text-gray-600 my-2">
                    {{ job.type }}
                </div>
                <h3 class="text-xl font-bold">
                    {{ job.title }}
                </h3>
            </div>
            
            <div class="mb-5">
                <div class="mb-1">
                    {{ truncatedDescription }}
                </div>
                <button 
                    @click="toggleDescription"
                    class="font-semibold text-sm text-green-500 hover:text-green-600"
                >
                    {{ showFullDescription ? 'Show Less' : 'Show More' }}
                </button>
            </div>

            <h3 class="font-semibold text-green-500 mb-2">
                {{ job.salary }}
            </h3>

            <div class="border border-gray-100 mb-5"></div>

            <div class="flex flex-col lg:flex-row justify-between">
                <div class="font-semibold text-orange-700 mb-3">
                    <i class="pi pi-map-marker text-orange-700"></i>
                    {{ job.location }}
                </div>
                <a 
                    :href="'/jobs/' + job.id" 
                    class="h-[36px] bg-green-500 hover:bg-green-600 text-white px-4 py-2 rounded-lg font-semibold text-center text-sm"
                >Read More
                </a>
            </div>
        </div>
    </div>
</template>