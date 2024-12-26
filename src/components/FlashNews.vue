<script setup lang="ts">
import Stack from '@/components/Stack.vue'
import { flashNews } from '@/mocks/news.ts'
import { ArrowRightIcon, ArrowLeftIcon } from '@heroicons/vue/24/solid'
import { computed, ref } from 'vue'

interface FlashNews {
  date: string
  rotate: number
  image: string
  id: number
  text: string
}

//slider
const isBackDirection = ref<boolean>(false)
const currentSlideIndex = ref<number>(0)
const currentSlide = computed(() => flashNews[currentSlideIndex.value])
const isLastSlide = computed(
  () => currentSlideIndex.value >= flashNews.length - 1
)

const nextSlide = () => {
  if (isLastSlide.value) {
    return
  }
  isBackDirection.value = false
  toggleLoading()
  currentSlideIndex.value++
}

const prevSlide = () => {
  if (currentSlideIndex.value === 0) {
    return 0
  }
  isBackDirection.value = true
  toggleLoading()
  currentSlideIndex.value--
}

//animation
const loading = ref<boolean>(false)
const toggleLoading = () => {
  loading.value = true
  setTimeout(() => {loading.value = false}, 300)
}
</script>

<template>
  <stack>
    <transition :name="!isBackDirection ? 'slide-fade' : 'slide-fade-reverse'">
    <div v-show="!loading" class="w-full bg-white rounded-2xl p-6 drop-shadow-md rotate-3">
      <div class="news-top">
        <img
          :src="currentSlide.image"
          class="rounded-2xl"
          alt="flash news poster"
        />
        <h2 class="text-orange mt-2 font-bold text-m">🔥Hot news</h2>
        <p class="mt-2 font-bold">
          {{ currentSlide.text }}
        </p>
      </div>
      <div class="news-footer mt-4 flex">
        <p class="text-gray-400 w-full">{{ currentSlide.date }}</p>
        <p class="text-gray-900 flex">
          <ArrowLeftIcon
            v-if="currentSlideIndex > 0"
            class="w-6 mr-2"
            @click="prevSlide"
          />
          {{ currentSlideIndex + 1 }}/{{ flashNews.length }}
          <ArrowRightIcon
            v-if="!isLastSlide"
            class="w-6 ml-2"
            @click="nextSlide"
          />
          <div class="w-6 ml-2" v-else></div>
        </p>
      </div>
    </div>
    </transition>
  </stack>
</template>

<style scoped>
.slide-fade-enter-active,
.slide-fade-reverse-enter-active,
.slide-fade-reverse-leave-active,
.slide-fade-leave-active
{
  transition: all .3s ease;
}

.slide-fade-enter {
  transform: translateX(100px);
  opacity: 0;
}
.slide-fade-leave-to {
  transform: translateX(-100px);
  opacity: 0;
}

.slide-fade-reverse-enter {
  transform: translateX(-100px);
  opacity: 0;
}
.slide-fade-reverse-leave-to {
  transform: translateX(100px);
  opacity: 0;
}

</style>
