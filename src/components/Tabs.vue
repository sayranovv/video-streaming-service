<script setup lang="ts">
import { Tab } from '@/types'

defineProps<{
  tabs: Tab[]
}>()
</script>

<template>
  <div>
    <nav class="flex space-x-4">
      <a
        v-for="{ id, emoji, title } in tabs"
        :key="id"
        class="bg-movie-black-200 rounded-lg px-4 py-2 text-white"
      >
        {{ emoji }}
        {{ title }}
      </a>
      <a>Comedy</a>
      <a>All</a>
    </nav>
  </div>
</template>
