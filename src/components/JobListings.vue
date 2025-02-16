<script setup lang="ts">
import JobListing from '@/components/JobListing.vue'
import type { Job } from '@/types/Job.ts'
import axios from 'axios'
import { onMounted, reactive } from 'vue'
import { RouterLink } from 'vue-router'

type Props = {
  limit?: number
  showButton?: boolean
}

withDefaults(defineProps<Props>(), {
  showButton: false,
})

const state = reactive({
  jobs: [] as Job[],
  isLoading: true,
})

const fetchJobs = async () => {
  try {
    const response = await axios('/api/jobs')
    state.jobs = (await response.data) as Job[]
  } catch (error) {
    console.error(error)
  } finally {
    state.isLoading = false
  }
}

onMounted(fetchJobs)
</script>

<template>
  <section class="bg-blue-50 px-4 py-10">
    <div class="m-auto container-xl lg:container">
      <h2 class="mb-6 text-center text-3xl font-bold text-green-500">Browse Jobs</h2>
    </div>

    <!-- Show loading spinner when isLoading is true -->
    <div v-if="state.isLoading" class="m-auto">
      <i class="pi pi-spin pi-spinner" style="font-size: 3rem"></i>
    </div>

    <!-- Show jobs when isLoading finished -->
    <div v-else class="grid grid-cols-1 gap-6 md:grid-cols-3">
      <JobListing
        v-for="job in state.jobs.slice(0, limit || state.jobs.length)"
        :key="job.id"
        :job="job"
      />
    </div>
  </section>

  <section v-if="showButton" class="m-auto my-10 max-w-lg px-6">
    <RouterLink
      to="/jobs"
      class="block rounded-xl bg-black px-6 py-4 text-center text-white hover:bg-gray-700"
      >View All Jobs
    </RouterLink>
  </section>
</template>
