<template>
  <header>
    <h1>{{title}} </h1>
    <Button @toggle-form="$emit('toggle-form')" :title="showAddForm ? 'Close' : 'Add Task'"
      :color="showAddForm ? 'red':'green'"></Button>
  </header>
</template>

<script>
import Button from './Button.vue';

export default {
  name: "Header",
  // props: ['title']
  props: { title: String, showAddForm: Boolean },
  components: { Button }
}
</script>

<style scoped>
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}
</style>