<script setup lang="ts">
import type { Tab } from '@/types'

defineProps<{
  tabs: Tab[]
  activeTab: string
}>()

const emits = defineEmits<{
  'on-tab-change': [tab: string]
}>()
</script>

<template>
  <div>
    <nav class="flex space-x-4">
      <a
        :class="id === activeTab ? 'bg-orange' : 'bg-movie-black-200'"
        v-for="{ id, emoji, title } in tabs"
        :key="id"
        class="text-lg rounded-lg px-4 py-2 text-white drop-shadow-sm hover:bg-orange cursor-pointer"
        @click="emits('on-tab-change', id)"
      >
        {{ emoji }}
        {{ title }}
      </a>
    </nav>
  </div>
</template>
