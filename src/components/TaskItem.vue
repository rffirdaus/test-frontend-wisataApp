<!-- eslint-disable vue/require-v-for-key -->
<!-- eslint-disable vue/no-mutating-props -->
<template>
  <div
    class="bg-gray-50 border-b border-gray-200"
  >
    <div
      v-for="(item, index) in task"
      class="my-4 flex items-center justify-between"
    >
      <div>
        <input
          type="checkbox"
          v-model="item.complete"
          @click="completeList(item.complete, index)"
          class="px-2 py-1 mr-2 border-black border-transparent focus:border-black border-solid border-2 focus:bg-white"
        />
        <span
          v-if="!item.edit"
          id="title"
          class="px-2 py-1 mr-2 w-40 border-transparent border-solid border-2 cursor-pointer"
          :class="item.cssLine"
          @click="completeList(item.complete, index)"
          >{{ item.title }}</span
        >
        <input
          v-else
          type="text"
          v-model="item.title"
          :ref="'task'"
          class="px-2 py-1 mr-2 w-40 border-black border-transparent focus:border-black border-solid border-2 focus:bg-white"
        />
      </div>
      <div class="flex">
        <button
          class="bg-orange-400 rounded-lg text-white hover:bg-black hover:text-orange-400 focus:bg-black focus:text-orange-400 px-2 py-2 mr-2"
          @click="deleteTask(item.id)"
        >
          Delete
        </button>
        <button
          class="bg-blue-400 rounded-lg text-white hover:bg-black hover:text-blue-400 focus:bg-black focus:text-blue-400 px-2 py-1"
          @click="enableEdit(index)"
        >
          {{!task[index].edit ? 'Edit' : 'Submit'}}
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    task: [Object, Array]
  },
  methods: {
    deleteTask (taskId) {
      this.$store.dispatch('deleteTask', taskId)
    },
    enableEdit (index) {
      if (!this.task[index].cssLine) {
        if (this.task[index].edit === false) {
        // eslint-disable-next-line vue/no-mutating-props
          this.task[index].edit = true
          this.$nextTick(() => {
            const input = this.$refs.task[0]
            input.focus()
          })
        } else {
          // eslint-disable-next-line vue/no-mutating-props
          this.task[index].edit = false
        }
      }
    },
    completeList (value, index) {
      if (!value) {
        // eslint-disable-next-line vue/no-mutating-props
        this.task[index].cssLine = 'line-through text-gray-300'
        // eslint-disable-next-line vue/no-mutating-props
        this.task[index].complete = true
      } else {
        // eslint-disable-next-line vue/no-mutating-props
        this.task[index].complete = false
        // eslint-disable-next-line vue/no-mutating-props
        this.task[index].cssLine = ''
      }
    }
  }
}
</script>
