<script setup lang="ts">
import TimeControl from '@/components/Player/TimeControl.vue'
import VolumeControl from '@/components/Player/VolumeControl.vue'
import { ref } from 'vue'

const videoDuration = ref<number>(0)
const videoCurrentTime = ref<number>(0)
const video = ref()
const player = ref()

const setVideoData = () => {
  if (video.value.readyState) {
    videoDuration.value = video.value.duration
  }
}

const progress = () => {
  videoCurrentTime.value = video.value.currentTime
}

const onTimeChange = (value: number) => {
  video.value.currentTime = value
  progress()
}

const onVolumeChange = (value: number) => {
  video.value.volume = value
}
</script>

<template>
  <div class="player max-w-[1024px]" ref="player">
    <video
      class="rounded-3xl"
      src="@/assets/brat.exe.mp4"
      controls
      preload="auto"
      ref="video"
      type="video/mp4"
      @loadedmetadata="setVideoData"
      @timeupdate="progress"
    />
    <TimeControl
      :video-duration="videoDuration"
      :current-video-position="videoCurrentTime"
      :is-active="true"
      @on-time-change="onTimeChange"
    />
    <VolumeControl @on-volume-change="onVolumeChange" />
  </div>
</template>

<style scoped>
.player {
  @apply w-full rounded-lg aspect-video relative object-cover cursor-pointer;
}

.video-screen {
  @apply aspect-video shadow-sm block w-full h-full cursor-pointer bg-movie-black-200;
}

::-webkit-media-controls {
  display: none;
}
</style>
