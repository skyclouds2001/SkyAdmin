<script setup lang="ts">
import { inject, type Ref } from 'vue'
import { useI18n } from 'vue-i18n'
import { ElBreadcrumb, ElBreadcrumbItem, ElImage, ElIcon } from 'element-plus'
import { Setting, FullScreen } from '@element-plus/icons-vue'
import { PROJECT_AUTHOR_NAME, PROJECT_AUTHOR_AVATAR } from '@/config'
import { useFullscreen } from '@/hook'
import { usePagesStore } from '@/store'

const i18n = useI18n()

const store = usePagesStore()

const { toggleFullscreen } = useFullscreen()

const isShowSettingDrawer = inject<Ref<boolean>>('setting')

/**
 * 控制展示设置窗口
 */
const showSettingDrawer = () => {
  if (isShowSettingDrawer) {
    isShowSettingDrawer.value = true
  }
}
</script>

<template>
  <div class="page-header">
    <el-breadcrumb>
      <el-breadcrumb-item v-for="item in store.pages" :key="item.name" :to="item.path">{{ i18n.t(`router.${item.path}`) }}</el-breadcrumb-item>
    </el-breadcrumb>

    <div class="control-bar">
      <div class="fullscreen" @click="toggleFullscreen">
        <el-icon :size="20"><FullScreen /></el-icon>
      </div>
      <div class="settings" @click="showSettingDrawer">
        <el-icon :size="20"><Setting /></el-icon>
      </div>
      <div class="username">{{ PROJECT_AUTHOR_NAME }}</div>
      <div class="avatar">
        <el-image :src="PROJECT_AUTHOR_AVATAR" fit="cover" loading="lazy" lazy alt="avatar" />
      </div>
    </div>
  </div>
</template>

<style scoped lang="scss">
.page-header {
  @apply flex justify-between items-center;

  height: 100%;

  .control-bar {
    @apply flex justify-center items-center;

    > * {
      @apply mx-1;
    }

    .fullscreen {
      @apply flex justify-center items-center;
    }

    .avatar {
      @apply w-8 h-8;
      @apply overflow-hidden;

      :deep(img) {
        @apply w-8 h-8;
        @apply rounded-full;
      }
    }

    .username {
      @apply cursor-default select-none;
    }

    .settings {
      @apply flex justify-center items-center;
    }
  }
}
</style>
