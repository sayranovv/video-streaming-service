<script setup lang="ts">
withDefaults(
  defineProps<{
    title?: string
    paddingless: boolean
  }>(),
  { padingless: false }
)
</script>

<template>
  <section
    class="bg-movie-black flex h-full min-x-0 flex-1 flex-col overflow-y-hidden"
  >
    <div class="mx-4 my-9 flex justify-between">
      <h1 v-if="title" class="text-4xl font-weight-900 font-bold text-white">
        {{ title }}
      </h1>
      <h1 v-else class="text-4xl font-weight-900 font-bold text-white">
        <slot name="title"></slot>
      </h1>
      <div>
        <slot name="header" />
      </div>
    </div>
    <div :class="paddingless ? '' : 'mx-4'">
      <slot />
    </div>
  </section>
</template>

<style scoped></style>
