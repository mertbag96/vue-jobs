<script setup>
import HomeCard from './HomeCard.vue'
</script>

<template>
    <section class="py-4">
      <div class="container-xl lg:container m-auto">
        <div class="grid grid-cols-1 md:grid-cols-2 gap-4 p-4 rounded-lg">
          <HomeCard>
            <h2 class="text-2xl font-bold">
                For Developers
            </h2>
            <p class="mt-2 mb-4">
                Browse our Vue jobs and start your career today
            </p>
            <a href="/jobs" class="inline-block bg-black text-white rounded-lg px-4 py-2 hover:bg-gray-700">
                <div class="flex items-center space-x-2">
                  <i class="pi pi-eye"></i>
                  <span>Browse Jobs</span>
                </div>
            </a>
          </HomeCard>

          <HomeCard bg="bg-green-100">
            <h2 class="text-2xl font-bold">
                For Employers
            </h2>
            <p class="mt-2 mb-4">
                List your job to find the perfect developer for the role
            </p>
            <a href="/add-job" class="inline-block bg-green-500 text-white rounded-lg px-4 py-2 hover:bg-green-600">
              <div class="flex items-center space-x-2">
                  <i class="pi pi-plus-circle"></i>
                  <span>Add Job</span>
                </div>
            </a>
          </HomeCard>
        </div>
      </div>
    </section>
</template>