<script setup lang="ts">
import Page from '@/components/layout/Page.vue'
import Tabs from '@/components/Tabs.vue'

import { tabs } from '@/mocks/tab.ts'
</script>

<template>
  <page>
    <template #title>Movie</template>
    <div>
      <tabs :tabs="tabs" />
    </div>
  </page>
</template>
