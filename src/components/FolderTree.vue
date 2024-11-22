<template>
  <div>
    <FolderNode
      v-for="folder in folders"
      :key="folder.id"
      :folder="folder"
      @select="handleSelect"
    />
  </div>
</template>

<script setup lang="ts">
import FolderNode from './FolderNode.vue'
import type { IFolder } from '@/types/folder'

const { folders } = defineProps<{
  folders: IFolder[]
}>()

const emit = defineEmits<{
  (e: 'select', folderId: number): void
}>()

const handleSelect = (folderId: number) => {
  emit('select', folderId)
}
</script>

<style scoped>
/* Минимальные стили */
</style>
