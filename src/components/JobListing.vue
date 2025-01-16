<script setup lang="ts">
import { computed, ref } from 'vue'
import type { Job } from '@/types/Job.ts'

const props = defineProps<{
  job: Job
}>()

const toggleFullDescription = () => {
  showFullDescription.value = !showFullDescription.value
}

const showFullDescription = ref(false)
const truncatedDescription = computed(() => {
  const description = props.job.description
  if (showFullDescription.value) {
    return description
  } else {
    return description.substring(0, 90) + ' ...'
  }
})
</script>

<template>
  <div class="relative rounded-xl bg-white shadow-md">
    <div class="p-4">
      <div class="mb-6">
        <div class="my-2 text-gray-600">{{ job.type }}</div>
        <h3 class="text-xl font-bold">{{ job.title }}</h3>
      </div>

      <div class="mb-5">
        <div>
          {{ truncatedDescription }}
        </div>
        <button
          class="mt-2 text-sm text-green-500 hover:text-green-600"
          @click="toggleFullDescription"
        >
          {{ showFullDescription ? 'Show less' : 'Show more' }}
        </button>
      </div>

      <h3 class="mb-2 text-green-500">{{ job.salary }}</h3>

      <div class="mb-5 border border-gray-100"></div>

      <div class="mb-4 flex flex-col justify-between lg:flex-row">
        <div class="mb-3 text-orange-700">
          <i class="pi pi-map-marker text-orange-700"></i>
          {{ job.location }}
        </div>
        <a
          :href="/job/ + job.id"
          class="rounded-lg bg-green-500 px-4 py-2 text-center text-sm text-white h-[36px] hover:bg-green-600"
        >
          Read More
        </a>
      </div>
    </div>
  </div>
</template>
