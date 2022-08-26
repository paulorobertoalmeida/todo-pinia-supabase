<template>
  <div>
    <div
      class="flex mb-4 items-center justify-between"
      v-for="(task, index) in tasks"
      :key="index"
    >
      <div class="">
        <p :class="task.is_complete ? 'done' : ''" class="todo-change-name w-full text-xl">
          {{ task.title }}
        </p>
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

      <div>
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
        <div
          class="
            relative
            inline-block
            w-10
            mx-2
            align-middle
            item-center
            select-none
            transition
            duration-200
            ease-in
          "
        >
          <input :class="task.is_complete ? 'todo-change-state' : 'todo-change-state-not'" @click="toggleReminderTask(task.id, index)"
            type="checkbox"
            name="toggle"
            id="toggle"
            class="
              toggle-checkbox
              absolute
              block
              w-6
              h-6
              rounded-full
              bg-white
              border-4
              appearance-none
              cursor-pointer
            "
          />
          <label
            for="toggle"
            class="
              toggle-label
              block
              overflow-hidden
              h-6
              rounded-full
              bg-gray-300
              cursor-pointer
            "
          ></label>
        </div>
        <label for="toggle" class="button text-xs text-gray-700"></label>
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
  //console.log(taskToEdit[index]);
  emit("change-name", taskToEdit[index]);
  name.value = "";
  changeNameActive.value = false;
};
</script>
<style>
/* CHECKBOX TOGGLE SWITCH */
/* @apply rules for documentation, these do not work as inline style */
.toggle-checkbox:checked {
  @apply: right-0 border-green-400;
  right: 0;
  border-color: #68d391;
}
.toggle-checkbox:checked + .toggle-label {
  @apply: bg-green-400;
  background-color: #68d391;
  text-decoration: line-through;
}
.todo-change-name:checked + .todo-label {
  @apply: ling-through
}

</style>