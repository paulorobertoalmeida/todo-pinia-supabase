<template>
  <form v-for="(task, index) in tasks" :key="index">
    <div class="flex mb-4 items-center">
      <div class="todo-title">
        <h3 :class="task.is_complete ? 'done' : ''" class="w-full text-grey-darkest">{{ task.title }}</h3>
      </div>

      <div class="todo-description">
        <p>{{ task.description }}</p>
      </div>
      <button
        @click="changeNameTask(task.id, index)"
        class="
          button
          flex-no-shrink
          p-2
          ml-4
          mr-2
          border-2
          rounded
          hover:text-white
          text-green
          border-green
          hover:bg-green
        "
      >
        Done
      </button>
      <button
        @click="deleteTask(task.id)"
        class="
          flex-no-shrink
          p-2
          ml-2
          border-2
          rounded
          text-red
         border-red hover:text-white hover:bg-red
        "
      >
        Remove
      </button>

      <div class="todo-buttons">
        <button
         :class="task.is_complete ? 'todo-change-state' : 'todo-change-state-not'" @click="toggleReminderTask(task.id, index)"
        > done</button>

        <div class="todo-change-name">
          <i
            class="change fas fa-edit fa-lg"
            @click="changeNameActiveValue"
          ></i>
        </div>

        <div class="todo-delete">
          <i class="change fas fa-ban fa-lg" @click="deleteTask(task.id)"></i>
        </div>
      </div>

      <div class="changeName" v-if="changeNameActive">
        <!-- @click="changeName(task.id, index)" -->
        <div class="add-task-form">
          <div class="input-field">
            <input
              class="input-field-input"
              type="text"
              placeholder="Edit title"
              v-model="name"
            />
          </div>
        </div>
      </div>
    </div>
  </form>
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
const idRef = ref(null);

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
const changeNameActiveValue = (id) => {
  idRef.value = id;
    changeNameActive.value = !changeNameActive.value;
};
const changeNameTask = (id, index) => {
  const taskToEdit = props.tasks.map((task) => 
  task.id === id ? {...task, title: name.value} : task
  );
  emit('change-name', taskToEdit[index]);
  name.value = "";
  changeNameActive.value = false;
};

</script>

<style>
</style>