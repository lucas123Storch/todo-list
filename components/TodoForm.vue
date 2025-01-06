<template>
  <div class="mt-4">
    <div class="p-4 border rounded-lg">
      <form @submit.prevent="addTask" class="space-y-4">
        <div class="flex gap-4">
          <input
            v-model="task"
            type="text"
            placeholder="Digite sua tarefa"
            class="flex-grow px-4 py-2 border rounded focus:outline-none focus:ring focus:ring-blue-300"
            :class="{'border-red-500': !valid && task.trim() === ''}"
          />

          <button
            :disabled="!valid || !task.trim()"
            type="submit"
            class="px-4 py-2 text-white bg-blue-500 rounded disabled:opacity-50 disabled:cursor-not-allowed hover:bg-blue-600"
          >
            Adicionar
          </button>
        </div>
        <p v-if="!valid && task.trim() === ''" class="text-sm text-red-500">A tarefa é obrigatória.</p>
      </form>
    </div>
  </div>
</template>

<script setup>
import { ref, defineEmits } from 'vue';
import { collection, addDoc } from 'firebase/firestore';
import Toastify from 'toastify-js';

const { $db } = useNuxtApp();

const emit = defineEmits(['taskAdded']);

const task = ref('');
const valid = ref(true);

const showToast = (message, type = 'success') => {
  Toastify({
    text: message,
    duration: 3000,
    gravity: 'top',
    position: 'center',
    style: {
      background: type === 'success' ? '#38a169' : '#e53e3e',
      color: '#fff',
    },
  }).showToast();
};

const addTask = async () => {
  if (!task.value.trim()) {
    valid.value = false;
    showToast('A tarefa não pode ser vazia.', 'error');
    return;
  }
  valid.value = true;

  try {
    const newTask = {
      text: task.value,
      completed: false,
      createdAt: new Date(),
    };
    const docRef = await addDoc(collection($db, 'tasks'), newTask);
    emit('taskAdded', { id: docRef.id, ...newTask });
    task.value = '';
    showToast('Tarefa adicionada com sucesso!', 'success');
  } catch (error) {
    console.error('Erro ao adicionar tarefa:', error);
    showToast('Erro ao adicionar tarefa.', 'error');
  }
};
</script>


<style scoped>
.disabled {
  opacity: 0.5;
  cursor: not-allowed;
}
</style>
