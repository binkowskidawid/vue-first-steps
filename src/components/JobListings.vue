<script setup lang="ts">
import jobsData from '@/jobs.json'
import type { Job } from '@/types/Job.ts'
import { ref } from 'vue'
import JobListing from '@/components/JobListing.vue'

type Props = {
  limit: number
  showButton?: boolean
}

withDefaults(defineProps<Props>(), {
  showButton: false,
})

const jobs = ref(jobsData.jobs as Job[])
</script>

<template>
  <section class="bg-blue-50 px-4 py-10">
    <div class="container-xl lg:container m-auto">
      <h2 class="text-3xl font-bold text-green-500 text-center mb-6">Browse Jobs</h2>
    </div>
    <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
      <JobListing v-for="job in jobs.slice(0, limit || jobs.length)" :key="job.id" :job="job" />
    </div>
  </section>

  <section v-if="showButton" class="m-auto max-w-lg my-10 px-6">
    <a
      href="/jobs"
      class="block bg-black text-white text-center py-4 px-6 rounded-xl hover:bg-gray-700"
      >View All Jobs</a
    >
  </section>
</template>
