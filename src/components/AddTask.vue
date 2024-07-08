<template>
  <div class="mb-4">
    <div class="flex">
      <input
        v-model="title"
        placeholder="Task title"
        class="flex-grow p-2 border border-gray-300 rounded-l-lg focus:outline-none focus:ring-2 focus:ring-blue-400"
      />
      <button
        @click="addTask"
        :disabled="!title"
        class=" text-white px-4 py-2 rounded-r-lg ml-2"
        :class="!title ? 'cursor-not-allowed bg-gray-300' : 'bg-blue-500 hover:bg-blue-600'"
      >
        Add Task
      </button>
    </div>
    <p class="error px-2 py-1 mt-4 rounded bg-red-200" v-if="isError">☝This task already exists.</p>
  </div>
</template>

<script>
import { mapGetters } from 'vuex'
export default {
  data () {
    return {
      title: '',
      isError: false
    }
  },
  computed: {
    ...mapGetters(['tasks'])
  },
  methods: {
    addTask () {
      const repeated = document.getElementById('title')
      const newTask = {
        id: Date.now(),
        title: this.title,
        completed: false,
        edit: false,
        cssLine: ''
      }
      // eslint-disable-next-line no-return-assign, no-sequences
      if (this.itemExist(this.title)) return this.isError = true, repeated.classList.add('bg-reds-200')
      if (repeated) {
        repeated.classList.remove('bg-orange-200')
      }
      this.isError = false
      this.$store.dispatch('addTask', newTask)
      this.title = ''
    },
    itemExist (value) {
      // eslint-disable-next-line no-var
      for (var i = 0; i < this.tasks.length; i++) {
        if (this.tasks[i].title === value) {
          return true
        }
      }

      return false
    }
  }
}
</script>
