<script setup lang="ts">
import { useRoute } from 'vue-router'
import {
  HomeIcon,
  FilmIcon,
  MagnifyingGlassCircleIcon
} from '@heroicons/vue/24/outline'
import {
  HomeIcon as HomeSolidIcon,
  FilmIcon as FilmSolidIcon,
  MagnifyingGlassCircleIcon as MagnifyingGlassCircleSolidIcon
} from '@heroicons/vue/24/solid'

const menu = [
  {
    to: '/',
    icon: HomeIcon,
    activeIcon: HomeSolidIcon
  },
  {
    to: '/search',
    icon: MagnifyingGlassCircleIcon,
    activeIcon: MagnifyingGlassCircleSolidIcon
  },
  {
    to: '/movies/1',
    icon: FilmIcon,
    activeIcon: FilmSolidIcon
  }
]

const router = useRoute()
</script>

<template>
  <nav class="block bg-movie-black-200">
    <div class="relative flex w-30 flex-col p-10 space-y-3">
      <router-link
        :to="to"
        v-for="{ to, icon, activeIcon, current } in menu"
        :key="to"
        :class="[
          router.path == to
            ? 'bg-movie-black-400 text-white'
            : 'text-gray-600 hover:bg-movie-black-400',
          'flex-shrink-0 inline-flex items-center justify-center h-14 w-14 rounded-lg'
        ]"
      >
        <component
          :is="router.path == to ? activeIcon : icon"
          class="h-6 w-6"
        />
      </router-link>
    </div>
  </nav>
</template>
