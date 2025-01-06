<template>
  <div class="min-h-screen bg-gray-100 flex items-center justify-center p-4">
    <div class="bg-white rounded-lg shadow-lg w-full max-w-3xl p-6">
      <h1 class="text-center font-bold text-2xl mb-6 text-orange-500">
        To-Do List
      </h1>

      <FormComponent />

      <ListComponent :tasks="tasks" />
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import FormComponent from '~/components/TodoForm.vue';
import ListComponent from '~/components/TodoList.vue';
import { collection, query, onSnapshot } from 'firebase/firestore';
const { $db } = useNuxtApp();

const tasks = ref([]);

const fetchTasks = () => {
  const q = query(collection($db, 'tasks'));
  onSnapshot(q, (snapshot) => {
    tasks.value = snapshot.docs.map((doc) => ({ id: doc.id, ...doc.data() }));
  });
};

fetchTasks();
</script>
