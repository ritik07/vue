<template>
  <button @click="$emit('toggle-form')" :style="{background:color}" class="btn">{{title}}</button>
</template>

<script>
export default {
  name: "Button",
  props: {
    title: String,
    color: String
  },
  emits: ['toggle-form'],
  methods: {
    handleAddTask() {
      console.log("clicked on add task")
    }
  }
}
</script> 