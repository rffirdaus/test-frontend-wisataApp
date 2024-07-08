<template>
  <div>
    <TaskItem :task="tasks" />
  </div>
</template>

<script>
import { mapGetters } from 'vuex'
import TaskItem from './TaskItem.vue'

export default {
  components: {
    TaskItem
  },
  computed: {
    ...mapGetters(['tasks'])
  }
}
</script>
