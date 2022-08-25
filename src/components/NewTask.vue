<template>
  <!-- component -->
  <form id="new-task" @submit.prevent="createNewTask">
    <div v-if="showErrorMessage">
      <p class="error-text text-white">{{ errorMessage }}</p>
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
              text-teal
              border-blue
              hover:text-white hover:bg-teal
            "
          >
            Submit
          </button>
        </div>
      </div>
      <!-- <div>
        <div class="flex mb-4 items-center">
          <p class="w-full text-grey-darkest">
            Add another component to Tailwind Components
          </p>
          <button
            class="
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
            class="
              flex-no-shrink
              p-2
              ml-2
              border-2
              rounded
              text-red
              border-red
              hover:text-white hover:bg-red
            "
          >
            Remove
          </button>
        </div>
        <div class="flex mb-4 items-center">
          <p class="w-full line-through text-green">
            Submit Todo App Component to Tailwind Components
          </p>
          <button
            class="
              flex-no-shrink
              p-2
              ml-4
              mr-2
              border-2
              rounded
              hover:text-white
              text-grey
              border-grey
              hover:bg-grey
            "
          >
            Not Done
          </button>
          <button class="flex-no-shrink
               ml-2
              border-2
              rounded
              text-red
              border-red
              hover:text-white hover:bg-red">Remove</button>
        </div>
      </div> -->
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
