<template>
  <div v-show="showAddForm">
    <form @submit="onSubmit" class="add-form">
      <div class="form-control">
        <label>Task</label>
        <input type="text" v-model="text" name="text" placeholder="Add Task" />
      </div>
      <div class="form-control">
        <label>Day & Time</label>
        <input type="text" v-model="day" name="day" placeholder="Add Day & Time" />
      </div>
      <div class="form-control form-control-check">
        <label>Set Reminder</label>
        <input type="checkbox" v-model="reminder" name="reminder" />
      </div>

      <input type="submit" value="Save Task" class="btn btn-block" />
    </form>
  </div>
</template>

<script>
export default {
  name: "AddTask",
  props: {
    task: [],
    showAddForm: Boolean
  },

  data() {
    return {
      text: '',
      day: '',
      reminder: '',
    }
  },

  emits: ['add-task'],

  methods: {
    onSubmit(e) {
      e.preventDefault()

      const payload = {
        id: this.task.length + 1,
        text: this.text,
        day: this.day,
        reminder: this.reminder
      }

      this.$emit('add-task', payload)

      this.text = ''
      this.day = ''
      this.reminder = ''

    }
  }

}
</script>

<style scoped>
.add-form {
  margin-bottom: 40px;
}

.form-control {
  margin: 20px 0;
}

.form-control label {
  display: block;
}

.form-control input {
  width: 100%;
  height: 40px;
  margin: 5px;
  padding: 3px 7px;
  font-size: 17px;
}

.form-control-check {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.form-control-check label {
  flex: 1;
}

.form-control-check input {
  flex: 2;
  height: 20px;
}
</style>