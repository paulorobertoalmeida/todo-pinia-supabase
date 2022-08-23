<template>
  <form id="new-task" @submit.prevent="createNewTask">
    <div v-if="showErrorMessage">
      <p class="error-text">{{ errorMessage }}</p>
    </div>
    <input
      v-model="name"
      type="text"
      name="new-task"
      class="input-field"
      minlength="4"
      placeholder="New Task"
    />
    <input
      v-model="description"
      type="text"
      name="new-task"
      class="input-field"
      minlength="4"
      placeholder="New Task"
    />
    <button @click.prevent="errorFunction" class="button">Submit</button>
  </form>
</template>

<script setup>
import { ref } from "vue";
import { useTaskStore } from "../stores/task";
// constant to save a variable that define the custom event that will be emitted to the homeView
const setTask = useTaskStore();
// constant to save a variable that holds the value of the title input field of the new task
const name = ref("");
// constant to save a variable that holds the value of the description input field of the new task
const description = ref("");
// constant to save a variable that holds an initial false boolean value for the errorMessage container that is
//conditionally displayed depending if the input field is empty
const showErrorMessage = ref(false);
// const constant to save a variable that holds the value of the error message
const errorMessage = ref(null);
const emit = defineEmits(["add-task"]);
// arrow function to call the form holding the task title and task description that uses a conditional to first
//checks if the task title is empty, if true the error message is displayed through the errorMessage container and sets
//a timeOut method that hides the error after some time. Else, its emmits a custom event to the home view with the task
//title and task description; clears the task title and task description input fields.
const errorFunction = () => {
  if (name.value.length === 0 || description.value.length === 0) {
    showErrorMessage.value = true;
    errorMessage.value = "The task title or description is empty";
    setTimeout(() => {
      // errorMessage.value = null;
      showErrorMessage.value = false;
    }, 5000);
  } else {
    const newTask = {
      name: name.value,
      description: description.value,
    };
    // console.log(newTask);
    emit("add-task", newTask);
    name.value = "";
    description.value = "";
    // setTask.addTask(name.value, description.value);
    // name.value = '';
    // description.value = '';
  }
};
</script>
<style></style>
