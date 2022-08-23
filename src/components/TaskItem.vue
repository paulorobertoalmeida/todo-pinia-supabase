<template>
  <div>
    <h1>{{ task.title }}</h1>
    <h2>{{ task.description }}</h2>
  </div>
</template>

<script setup>

const emits = defineEmits(["childDelete", "childReminder", "childEdit"]);
const props = defineProps(["task"]);
const deleteTask = () => {
  if(confirm("are u sure u want to delete?")){
    taskStore.deleteTask(task.user_id);
  }
};

</script>

<style>
</style>