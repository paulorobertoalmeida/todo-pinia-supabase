<template>
  <!-- component -->
  <form id="new-task" @submit.prevent="createNewTask">
    <div v-if="showErrorMessage">
      <p class="error-text text-red-500">{{ errorMessage }}</p>
    </div>
    <div>
      <div class="mb-4">
        <h1 class="text-grey-darkest">My Todo List - {{ date }}</h1>
        <div class="flex mt-4">
          <input
            v-model="name"
            class="
              shadow
              appearance-none
              border
              rounded
              w-full
              py-2
              px-3
              mr-4
              text-grey-darker
            "
            placeholder="Task Title"
          />
          <br />
          <input
            v-model="description"
            class="
              shadow
              appearance-none
              border
              rounded
              w-full
              py-2
              px-3
              mr-4
              text-grey-darker
            "
            placeholder="New Task"
          />
          <button
            @click.prevent="errorFunction"
            class="
              button
              flex-no-shrink
              p-2
              border-2
              rounded
              text-green-700
              border-green-700
              hover:text-white hover:bg-green-700
            "
          >
            Submit
          </button>
        </div>
      </div>
    </div>
  </form>
</template>

<script setup>
import moment from "moment";
import { ref } from "vue";
import { useTaskStore } from "../stores/task";

const date = moment().format("ll");
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
<style>
</style>
