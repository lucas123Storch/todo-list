<template>
  <div class="p-4 bg-white rounded-lg shadow">
    <ul class="space-y-4">
      <li
        v-for="task in tasks"
        :key="task.id"
        class="flex items-center justify-between p-4 bg-gray-100 rounded"
      >
        <div class="flex items-center">
          <input
            type="checkbox"
            v-model="task.completed"
            @change="toggleCompleted(task)"
            class="mr-4 h-5 w-5 text-blue-500 focus:ring focus:ring-blue-300"
          />
          <span
            :class="{
              'line-through text-gray-500': task.completed,
              'text-gray-900': !task.completed,
            }"
            class="text-lg"
          >
            {{ task.text }}
          </span>
        </div>
        <button
          @click="deleteTask(task)"
          class="px-3 py-2 text-sm font-medium text-white bg-red-500 rounded hover:bg-red-600"
        >
          Remover
        </button>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref, onMounted, defineProps } from 'vue';
import { collection, query, onSnapshot, doc, updateDoc, deleteDoc } from 'firebase/firestore';
import Toastify from 'toastify-js';

const { $db } = useNuxtApp();

const props = defineProps({
  tasks: {
    type: Array,
    required: true,
  },
});

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

const toggleCompleted = async (task) => {
  try {
    const taskRef = doc($db, 'tasks', task.id);
    await updateDoc(taskRef, {
      completed: task.completed,
    });
    showToast(
      `Tarefa "${task.text}" marcada como ${
        task.completed ? 'completa' : 'incompleta'
      }.`,
      'success'
    );
  } catch (error) {
    console.error('Erro ao atualizar tarefa:', error);
    showToast('Erro ao atualizar tarefa.', 'error');
  }
};

const deleteTask = async (task) => {
  try {
    const taskRef = doc($db, 'tasks', task.id);
    await deleteDoc(taskRef);
    showToast(`Tarefa "${task.text}" removida com sucesso!`, 'success');
  } catch (error) {
    console.error('Erro ao remover tarefa:', error);
    showToast('Erro ao remover tarefa.', 'error');
  }
};
</script>

<style scoped>
.text-decoration-line-through {
  text-decoration: line-through;
}
</style>
