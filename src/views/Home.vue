<template>
    <Nav />
    <div class="bg-black 
      w-full
      flex
      items-center
      justify-center
      bg-teal-lightest
      font-sans
      h-100">
      <div class="bg-white rounded shadow  m-4 w-full lg:w-3/4 lg:max-w-lg
   p-6">
        <NewTask @add-task="setNewTask" />
        <TaskItem
          :tasks="addNewTask.tasks"
          @toggle-reminder="toggleReminder"
          @delete-task="deleteTaskArr"
        />
      </div>
    </div>
    <Footer />
  
</template>

<script setup>
// 1. ref() is used here!
import { ref } from "vue";
import { useTaskStore } from "../stores/task";
import Nav from "../components/Nav.vue";
import TaskItem from "../components/TaskItem.vue";
import NewTask from "../components/NewTask.vue";
import Footer from "../components/Footer.vue";

const addNewTask = useTaskStore();
// onMounted(() => addNewTask.fetchTasks());
// async created(){
//   addNewTask.tasks = await addNewTask.fetchTasks();
// };
addNewTask.fetchTasks();
// console.log(addNewTask.tasks)
async function setNewTask(task) {
  await addNewTask.addTask(task.name, task.description);
}
async function toggleReminder(task) {
  // addNewTask.tasks = addNewTask.tasks.map((task) =>
  // task.user_id === id ? {...task, is_complete: !task.is_complete} : task
  // );
  // await addNewTask.toggleTask();
  console.log(task);
}
async function deleteTaskArr(task) {
  // await addNewTask.deleteTask();
}
</script>

<style>
</style>