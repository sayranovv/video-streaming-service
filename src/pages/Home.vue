<script setup lang="ts">
import Page from '@/components/layout/Page.vue'
import Tabs from '@/components/Tabs.vue'
import { tabsMock } from '@/mocks/tabs'
import { ref } from 'vue'
import MainBanner from '@/components/MainBanner.vue'
import FlashNews from '@/components/FlashNews.vue'
import ContentRow from '@/components/ContentRow.vue'

const activeTab = ref<string>(tabsMock[0].id)
const onTabChange = (tabId: string) => {
  activeTab.value = tabId
}
</script>

<template>
  <Page>
    <template #title>Movie</template>
    <div>
      <Tabs
        :tabs="tabsMock"
        :active-tab="activeTab"
        @on-tab-change="onTabChange"
      />
    </div>
    <content-row>
      <MainBanner />
      <div class="ml-10 max-w-md w-full">
        <FlashNews />
      </div>
    </content-row>
  </Page>
</template>
