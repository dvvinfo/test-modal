<template>
  <div class="container">
    <button @click="openModal">Открыть</button>
    <FolderModal
      v-if="isModalOpen"
      :title="modalTitle"
      :folders="mockFolders"
      @close="closeModal"
      @select="handleSelect"
    />
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import FolderModal from './components/FolderModal.vue'

const isModalOpen = ref(false)
const modalTitle = 'Выберите папку'

const mockFolders = [
  {
    id: 1,
    name: 'Папка 1',
    children: [
      { id: 2, name: 'Папка 1.1', children: [] },
      { id: 3, name: 'Папка 1.2', children: [{ id: 4, name: 'Папка 1.2.1', children: [] }] },
    ],
  },
  { id: 5, name: 'Папка 2', children: [
      { id: 6, name: 'Папка 2.1', children: [] },
      { id: 7, name: 'Папка 2.2', children: [{ id: 8, name: 'Папка 2.2.1', children: [] }] },
    ], },
]

const openModal = () => {
  isModalOpen.value = true
}

const closeModal = () => {
  isModalOpen.value = false
}

const handleSelect = (folderId: number) => {
  console.log('Selected folder ID:', folderId)
  closeModal()
}
</script>

<style>
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}
button {
  padding: 10px 20px;
  font-size: 20px;
  background-color: rgb(71, 71, 241);
  color: #fff;
  border: none;
}
</style>
