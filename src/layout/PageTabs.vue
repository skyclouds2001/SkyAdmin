<script setup lang="ts">
import { onBeforeMount } from 'vue'
import { useRoute, useRouter } from 'vue-router'
import { ElTabs, ElTabPane, ElScrollbar } from 'element-plus'
import { useTabsStore } from '@/store'

const route = useRoute()

const router = useRouter()

const store = useTabsStore()

/**
 * 切换 Tab 方法
 *
 * @param path - 待切换 tab 对应页面路径
 */
const switchTab = (path: string) => {
  router.push(path)
}

/**
 * 移除 Tab 方法
 *
 * @param path - 该 tab 对应页面路径
 */
const removeTab = (path: string) => {
  const index = store.tabs.findIndex((v) => v.path === path)
  store.tabs.splice(index, 1)
  if (store.currentTab === path) {
    store.currentTab = store.tabs[0].path
  }
}

onBeforeMount(() => {
  store.currentTab = route.path
})
</script>

<template>
  <el-tabs v-model="store.currentTab" class="tabs" type="border-card" @tab-change="switchTab" @tab-remove="removeTab">
    <el-tab-pane v-for="item in store.tabs" :key="item.path" class="tab" :label="item.name" :name="item.path" lazy :closable="item.path !== '/'">
      <el-scrollbar>
        <slot v-if="item.path === store.currentTab" />
      </el-scrollbar>
    </el-tab-pane>
  </el-tabs>
</template>

<style scoped lang="scss">
.tabs {
  @apply w-full h-full;
  @apply border-0;

  .tab {
    width: 100%;
    height: calc(100vh - 60px * 2 - 40px);
  }
}
</style>

<style>
div:has(.tab) {
  padding: 0 !important;
}
</style>