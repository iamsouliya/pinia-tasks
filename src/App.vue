<template>
  <main>
    <header>
      <img src="./assets/pinia-logo.svg" alt="pinia logo" />
      <h1>Pinia Task</h1>
    </header>

    <div class="new-task-form">
      <TaskForm />
    </div>

    <nav class="filter">
      <button @click="filter = 'all'">All Tasks</button>
      <button @click="filter = 'fav'">Fav Tasks</button>
    </nav>

    <div class="loading" v-if="isLoading">Loading tasks...</div>

    <div class="task-list" v-if="filter === 'all'">
      <p>Your have {{ totalCount }} tasks left to do</p>
      <div v-for="task in tasks" :key="task.id">
        <TaskDetails :task="task" />
      </div>
    </div>
    <div class="task-list" v-if="filter === 'fav'">
      <p>Your have {{ favCount }} tasks left to do</p>
      <div v-for="task in favs" :key="task.id">
        <TaskDetails :task="task" />
      </div>
    </div>
    <div class="wrapper">
      <button class="button-1" @click="taskStore.$reset">reset state</button>
    </div>
  </main>
</template>

<script setup lang="ts">
  import { useTaskStore } from './stores/TaskStore'
  import TaskDetails from './components/TaskDetails.vue'
  import { ref } from 'vue'
  import TaskForm from './components/TaskForm.vue'
  import { storeToRefs } from 'pinia'

  const taskStore = useTaskStore()

  const { tasks, isLoading, favs, totalCount, favCount } =
    storeToRefs(taskStore)

  taskStore.getTasks()
  const filter = ref('all')
</script>

<style scoped>
  /* CSS */
  .button-1 {
    background: #ffd859;
    border: 0;
    padding: 10px;
    font-family: 'Poppins';
    border-radius: 6px;
    cursor: pointer;
    font-size: 1em;
  }
  .wrapper {
    display: flex;
    justify-content: center;
  }
</style>
