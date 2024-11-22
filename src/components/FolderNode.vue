<template>
  <div>
    <div @click="toggle" class="folder-node">
      <div class="folder-node-input">
        <input type="radio" :value="folder.id" v-model="selectedFolderId" @change="selectFolder" />
        <span>{{ folder.name }}</span>
      </div>
      <button v-if="folder.children.length" @click.stop="toggleChildren">
        {{ isOpen ? '-' : '+' }}
      </button>
    </div>
    <div v-if="isOpen && folder.children.length">
      <FolderNode
        v-for="child in folder.children"
        :key="child.id"
        :folder="child"
        @select="handleSelect"
      />
    </div>
  </div>
</template>

<script setup lang="ts">
import type { IFolder } from '@/types/folder';
import { ref} from 'vue'

const { folder } = defineProps<{
  folder: IFolder;
}>()

const emit = defineEmits<{
  (e: 'select', folderId: number): void
}>()

const isOpen = ref(false)
const selectedFolderId = ref<number | null>(null)

const toggle = () => {
  isOpen.value = !isOpen.value
}

const toggleChildren = () => {
  isOpen.value = !isOpen.value
}

const selectFolder = () => {
  emit('select', folder.id)
}

const handleSelect = (folderId: number) => {
  emit('select', folderId)
}
</script>

<style scoped>
.folder-node {
  cursor: pointer;
  padding: 5px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 10px;
}

.folder-node-input {
  display: flex;
  align-items: center;
  gap: 8px;
}

.folder-node button {
  border: none;
  background-color: rgb(71, 71, 241);
  color: white;
  padding: 5px 10px;
  cursor: pointer;
  min-width: 32px;
}
</style>
