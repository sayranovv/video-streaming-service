<script setup lang="ts">
import 'vue3-carousel/dist/carousel.css'
import { Carousel, Slide } from 'vue3-carousel'
import { movies } from '@/mocks/movies.ts'
import MovieCard from '@/components/MovieCard.vue'
</script>

<template>
  <div class="mt-6">
    <carousel :items-to-show="3.5">
      <slide v-for="movie in movies" :key="movie.id">
        <MovieCard v-bind="movie" link="#" />
      </slide>
    </carousel>
  </div>
</template>

<style>
.carousel__viewport {
  @apply pl-4;
}
</style>
