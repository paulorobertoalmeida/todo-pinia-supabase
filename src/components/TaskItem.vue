<template>
  <div >
    <div class="flex mb-4 items-center" v-for="(task, index) in tasks" :key="index">
      <div>
        <p :class="task.is_complete ? 'done' : ''" class="w-full text-xl">
          {{ task.title }}
        </p>
        <div
          :class="
            task.is_complete ? 'todo-change-state' : 'todo-change-state-not'
          "
          @click="toggleReminderTask(task.id, index)"
        ></div>

        <div v-if="changeNameActive && idRef === task.id">
          <input
            class="input-field-input"
            type="text"
            placeholder="Edit title"
            v-model="name"
          />
        </div>
        <div>
          <p class="text-sm">{{ task.description }}</p>
        </div>
      </div>

      <div class="flex space-between">
        <button
          class="
            button
            flex-no-shrink
            p-2
            ml-2
            border-2
            rounded
            text-gray-500
            border-gray-500
            hover:text-white hover:bg-gray-500
          "
          @click="changeNameActiveValue(task.id)"
        >
          Edit
        </button>
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
            text-green-700
            border-green-700
            hover:bg-green-700
          "
        >
          Done
        </button>
        <button
          @click="deleteTask(task.id)"
          class="
          button
            flex-no-shrink
            p-2
            ml-2
            border-2
            rounded
            text-red-500
            border-red-500
            hover:text-white hover:bg-red-500
          "
        >
          Remove
        </button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
const emit = defineEmits(["toggle-reminder", "delete-task", "change-name"]);
const props = defineProps({
  tasks: Array,
});

const name = ref("");
const description = ref("");

const changeNameActive = ref(false);
const idRef = ref(null);

const toggleReminderTask = (id, index) => {
  const taskToToggle = props.tasks.map((task) =>
    task.id === id ? { ...task, is_complete: !task.is_complete } : task
  );
  emit("toggle-reminder", taskToToggle[index]);
};
const deleteTask = (id) => {
  const taskToDelete = props.tasks.filter((task) => task.id === id);
  emit("delete-task", taskToDelete[0]);
};
const changeNameActiveValue = (id) => {
  idRef.value = id;
  changeNameActive.value = !changeNameActive.value;
};
const changeNameTask = (id, index) => {
  const taskToEdit = props.tasks.map((task) =>
    task.id === id ? { ...task, title: name.value } : task
  );
  emit("change-name", taskToEdit[index]);
  name.value = "";
  changeNameActive.value = false;
};
</script>

<style>
</style>