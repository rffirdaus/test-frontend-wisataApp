<template>
  <div class="app-container min-h-screen bg-gray-100 p-4 flex flex-col items-center">
    <div class="w-full max-w-lg bg-white rounded-lg shadow-md p-6">
      <h1 class="text-2xl font-bold">Todo List App</h1>
      <p class="text-base mb-8">You have {{ tasks.length }} tasks.</p>
      <AddTask />
      <TaskList />
    </div>
  </div>
</template>

<script>
import { mapGetters } from 'vuex'
import AddTask from '../components/AddTask.vue'
import TaskList from '../components/TaskList.vue'

export default {
  components: {
    AddTask,
    TaskList
  },
  computed: {
    ...mapGetters(['tasks'])
  }
}
</script>
