<template>
  <form @submit.prevent="handleSubmit">
    <input placeholder="I need to..." v-model="newTask" type="text" />
    <button>Add</button>
  </form>
</template>

<script setup lang="ts">
  import { useTaskStore } from '@/stores/TaskStore'
  import { ref } from 'vue'

  const TaskStore = useTaskStore()
  const newTask = ref('')

  const handleSubmit = () => {
    if (newTask.value.length > 0) {
      TaskStore.addTask({
        title: newTask.value,
        isFav: false,
        id: Math.floor(Math.random() * 1000000),
      })
    }
    newTask.value = ''
  }
</script>
