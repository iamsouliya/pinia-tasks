<template>
  <div class="task">
    <h3>
      {{ task.title }}
    </h3>
    <div class="icons">
      <i class="material-icons" @click="TaskStore.removeTask(task.id)">
        delete
      </i>
      <i
        class="material-icons"
        :class="{ active: task.isFav }"
        @click="TaskStore.toggleFav(task.id)"
      >
        favorite
      </i>
    </div>
  </div>
</template>

<script setup lang="ts">
  import type { PropType } from 'vue'
  import type { Task } from '@/types/Task'
  import { useTaskStore } from '@/stores/TaskStore'

  defineProps({
    task: {
      type: Object as PropType<Task>,
      required: true,
    },
  })
  const TaskStore = useTaskStore()
</script>
