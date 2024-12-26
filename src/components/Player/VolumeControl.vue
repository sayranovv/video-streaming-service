<script setup lang="ts">
import { SpeakerWaveIcon, SpeakerXMarkIcon } from '@heroicons/vue/24/solid'
import { ref, computed } from 'vue'

const volumeLevel = ref(50)

const volumeLevel1 = computed(() => `${volumeLevel.value}% 100%`)

const emits = defineEmits<{ 'on-volume-change': { value: number } }>()

const adjustVolume = () => {
  emits('on-volume-change', volumeLevel.value / 100)
}
</script>

<template>
  <div class="volume-container">
    <SpeakerWaveIcon
      v-if="volumeLevel > 0"
      @click="volumeLevel = 0"
      class="rotate-90 text-white w-[25px] mr-4"
    />
    <SpeakerXMarkIcon
      v-else
      @click="volumeLevel = 50"
      class="rotate-90 text-white w-[25px] mr-4"
    />
    <input
      type="range"
      class="volume-slider"
      min="0"
      max="100"
      @change="adjustVolume"
      @mouseleave="adjustVolume"
      v-model="volumeLevel"
    />
  </div>
</template>

<style scoped>
.volume-container {
  @apply bg-gray-600 absolute bottom-2/4 -rotate-90 right-[-40px] flex p-4 rounded-lg bg-opacity-10;
}

.volume-slider {
  @apply h-[8px] w-full outline-none self-center opacity-70 cursor-pointer rounded-2xl;
  background-image: linear-gradient(#f37515, #f37515);
  background-repeat: no-repeat;
  background-size: v-bind(volumeLevel1);
  -webkit-appearance: none;
}

.volume-slider::-webkit-slider-thumb {
  @apply h-[18px] w-[18px] self-center bg-orange rounded-lg cursor-pointer outline-none;
  -webkit-appearance: none;
}

.volume-slider::-moz-range-thumb {
  @apply h-[18px] w-[18px] self-center bg-orange rounded-lg cursor-pointer outline-none;
  -webkit-appearance: none;
}
</style>
