<template>
  <div class="modal" @click="closeModal">
    <div class="modal-content" @click.stop>
      <h2>{{ title }}</h2>
      <FolderTree :folders="folders" @select="handleSelect" />
      <div class="modal-actions">
        <button @click="closeModal" class="close-button">Закрыть</button>
        <button @click="confirmSelection" class="confirm-button">Ок</button>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import FolderTree from './FolderTree.vue';
import type { IFolder } from '@/types/folder';



const { title, folders } = defineProps<{
  title: string;
  folders: IFolder[];
}>();

const emit = defineEmits<{
  (e: 'close'): void;
  (e: 'select', folderId: number): void;
}>();

const closeModal = () => {
  emit('close');
};

const confirmSelection = () => {
  if (selectedFolderId.value !== null) {
    emit('select', selectedFolderId.value);
    console.log('Selected folder ID:', selectedFolderId.value);

  }
  closeModal();
};

const selectedFolderId = ref<number | null>(null);

const handleSelect = (folderId: number) => {
  selectedFolderId.value = folderId;
};
</script>

<style scoped>
.modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal-content {
  background: white;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
  min-width: 300px;
}

.modal-actions {
  display: flex;
  justify-content: flex-end;
  margin-top: 20px;
}

.modal-actions button {
  margin-left: 10px;
}
.close-button {
  background-color: #13c213;
  color: #fff;
  border: none;
}
.confirm-button {
  background-color: rgb(71, 71, 241);
  color: #fff;
  border: none;
}
</style>
