<template>
  <div class="bg-black">
    <Nav />
    <div
      class="
        h-screen
        bg-black
        w-full
        flex
        items-center
        justify-center
        bg-teal-lightest
        font-sans
      "
    >
      <div ><SearchBar />
        <NewTask @add-task="setNewTask" />
        <TaskItem
          :tasks="addNewTask.tasks"
          @toggle-reminder="toggleReminder"
          @delete-task="deleteTaskArr"
          @change-name="changeName"
        />
      </div>
    </div>
    <Footer />
  </div>
</template>

<script setup>

import { ref } from "vue";
import { useTaskStore } from "../stores/task";
import Nav from "../components/Nav.vue";
import TaskItem from "../components/TaskItem.vue";
import SearchBar from "../components/SearchBar.vue";
import NewTask from "../components/NewTask.vue";
import Footer from "../components/Footer.vue";

const addNewTask = useTaskStore();

addNewTask.fetchTasks();
console.log(addNewTask.tasks);
async function setNewTask(task) {
  await addNewTask.addTask(task.name, task.description);
  addNewTask.fetchTasks();
}
async function toggleReminder(task) {
  await addNewTask.toggleTask(task.is_complete, task.id);
  addNewTask.fetchTasks();
}
async function deleteTaskArr(task) {
  await addNewTask.deleteTask(task.id);
  addNewTask.fetchTasks();
}
async function changeName(task) {
  await addNewTask.editTask(task.title, task.id);
  addNewTask.fetchTasks();
}
</script>

<style>
</style>