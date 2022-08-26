<template>
  <!-- component -->
  <form id="new-task" @submit.prevent="createNewTask">
    <div v-if="showErrorMessage">
      <p class="error-text text-red-500">{{ errorMessage }}</p>
    </div>
    <div class="">
      <div class="mb-4">
        <h1 class="font-mono text-2xl">My Todo List - {{ date }}</h1>
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

const setTask = useTaskStore();

const name = ref("");

const description = ref("");

const showErrorMessage = ref(false);

const errorMessage = ref(null);
const emit = defineEmits(["add-task"]);

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
    
  }
};
</script>
<style>
</style>
