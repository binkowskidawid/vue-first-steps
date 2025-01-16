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
    <div class="m-auto container-xl lg:container">
      <h2 class="mb-6 text-center text-3xl font-bold text-green-500">Browse Jobs</h2>
    </div>
    <div class="grid grid-cols-1 gap-6 md:grid-cols-3">
      <JobListing v-for="job in jobs.slice(0, limit || jobs.length)" :key="job.id" :job="job" />
    </div>
  </section>

  <section v-if="showButton" class="m-auto my-10 max-w-lg px-6">
    <a
      href="/jobs"
      class="block rounded-xl bg-black px-6 py-4 text-center text-white hover:bg-gray-700"
      >View All Jobs</a
    >
  </section>
</template>
