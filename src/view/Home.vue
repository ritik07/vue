<template>
  <AddTask :showAddForm="showAddForm" :task="task" @add-task="addTask"></AddTask>
  <Tasks @toggle-reminder="toggleReminder" @delete-task="deleteTask" :tasks="task"></Tasks>
</template>

<script>
import Tasks from '../components/Tasks.vue'
import AddTask from '../components/AddTask.vue'

export default {
  name: "Home",
  props: {
    showAddForm: Boolean
  },
  components: {
    Tasks,
    AddTask,
  },
  
  data() {
    return {
      task: [],
    }
  },

  methods: {
    deleteTask(id) {
      this.task = this.task.filter((x) => x.id !== id)
    },

    toggleReminder(id) {
      this.task = this.task.map((item) => item.id == id ? { ...item, reminder: !item.reminder } : item)
    },

    async addTask(payload) {
      let res = await fetch('api/task', {
        method: 'POST',
        headers: { 'Content-type': 'application/json' },
        body: JSON.stringify(payload)
      })

      const data = await res.json()
      console.log("data", data)
      this.task = await this.fetchData()
    },

    async fetchData() {
      const res = await fetch('api/task')
      const data = await res.json()
      return data
    }
  },

  async created() {
    this.task = await this.fetchData()
  }
}
</script>