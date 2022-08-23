<template>
    <form
    id="new-task"
    @submit.prevent="createNewTask"
  >
    <input
      v-model="title"
      type="text"
      name="new-task"
      class="text"
      minlength="4"
      placeholder="New Task"
    >
    <button class="submit">
      Submit
    </button>
  </form>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { useUserStore} from "@/stores/user";
import {useUserTask} from "@/stores/task";
// constant to save a variable that define the custom event that will be emitted to the homeView


// constant to save a variable that holds the value of the title input field of the new task
const title = ref(null);
// constant to save a variable that holds the value of the description input field of the new task
const taskStore = userTaskStore();

// constant to save a variable that holds an initial false boolean value for the errorMessage container that is conditionally displayed depending if the input field is empty
const errorInput = () => {
  title.value = "";
};

// const constant to save a variable that holds the value of the error message

// arrow function to call the form holding the task title and task description that uses a conditional to first checks if the task title is empty, if true the error message is displayed through the errorMessage container and sets a timeOut method that hides the error after some time. Else, its emmits a custom event to the home view with the task title and task description; clears the task title and task description input fields.


async function createNewTask() {
  try {
    console.log(title.value)
    await taskStore.createTask(title.value, userStore.user.id)
    clearInput()
  } catch (e) {
    alert('could not add task')
  }
}
</script>

<style></style>
