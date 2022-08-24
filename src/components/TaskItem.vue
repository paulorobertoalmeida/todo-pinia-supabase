<template>
  <div class="container">

    <div class="todo-item" v-for="(task, index) in tasks" :key="index">
      <div class="todo-image">
        <i class="task fas fa-tasks fa-lg"></i>
      </div>

      <div class="todo-container">
        <div class="todo-title">
          <h3>{{ task.title }}</h3>
        </div>

        <div class="todo-description">
          <p>{{ task.description }}</p>
        </div>

        <div class="todo-buttons">
          <div :class="task.is_complete ? 'todo-change-state' : 'todo-change-state-not'" @click="toggleReminderTask(task.id, index)"></div>

          <div class="todo-change-name">
            <i class="change fas fa-edit fa-lg" @click="changeNameActiveValue"></i>
          </div>

          <div class="todo-delete">
            <i class="change fas fa-ban fa-lg" @click="deleteTask(task.id)"></i>
          </div>
        </div>

        <div class="changeName" v-if="changeNameActive">
          <!-- @click="changeName(task.id, index)" -->
          <div class="add-task-form">
            <div class="input-field">
              <input class="input-field-input" type="text" placeholder="Edit title" v-model="name">
            </div>
          </div>
        </div>

      </div>
    </div>
  </div>
  <div>
            <div class="flex mb-4 items-center">
                <p class="w-full text-grey-darkest">Add another component to Tailwind Components</p>
                <button @click="changeNameTask(task.id, index)" class="button flex-no-shrink p-2 ml-4 mr-2 border-2 rounded hover:text-white text-green border-green hover:bg-green">Done</button>
                <button class="flex-no-shrink p-2 ml-2 border-2 rounded text-red border-red hover:text-white hover:bg-red">Remove</button>
            </div>
          	<div class="flex mb-4 items-center">
                <p class="w-full line-through text-green">Submit Todo App Component to Tailwind Components</p>
                <button class="flex-no-shrink p-2 ml-4 mr-2 border-2 rounded hover:text-white text-grey border-grey hover:bg-grey">Not Done</button>
                <button class="flex-no-shrink p-2 ml-2 border-2 rounded text-red border-red hover:text-white hover:bg-red">Remove</button>
            </div>
        </div>
</template>

<script setup>

import { ref } from 'vue'
const emit = defineEmits(['toggle-reminder', 'delete-task', 'change-name']);
const props = defineProps({
  tasks: Array,
});

const name = ref('');
const description = ref('');

const changeNameActive = ref(false);

const toggleReminderTask = (id, index) => {
 
  const taskToToggle = props.tasks.map((task) =>
  task.id === id ? {...task, is_complete: !task.is_complete} : task
  );
  emit('toggle-reminder', taskToToggle[index]);
};
const deleteTask = (id) => {
  const taskToDelete = props.tasks.filter((task) => task.id === id);
  emit('delete-task', taskToDelete[0]);
};
const changeNameActiveValue = () => {
  changeNameActive.value = !changeNameActive.value;
};
const changeNameTask = (id, index) => {
  const taskToEdit = props.tasks.map((task) => 
  task.id === id ? {...task, title: name.value} : task
  );
  emit('change-name', taskToEdit[index]);
  name.value = "";
};
</script>

<style>
</style>