<template>
<!-- component -->
<!-- page -->
<main
  class="mx-auto flex min-h-screen w-full items-center justify-center bg-gray-900 text-white"
>
  <!-- component -->
  <section class="flex w-[30rem] flex-col space-y-10" @submit.prevent="signUp">
    <div class="text-center text-4xl font-medium">Sign Up</div>

    <div
      class="w-full transform border-b-2 bg-transparent text-lg duration-300 focus-within:border-indigo-500"
    >
      <input
        :type="text"
        placeholder="Email or Username"
        class="w-full border-none bg-transparent outline-none placeholder:italic focus:outline-none"
      />
    </div>

    <div
      class="w-full transform border-b-2 bg-transparent text-lg duration-300 focus-within:border-indigo-500"
    >
      <input
        type="password"
        v-model="password"
        placeholder="Password"
        class="w-full border-none bg-transparent outline-none placeholder:italic focus:outline-none"
      />
    </div>
    <div w-full transform border-b-2 bg-transparent text-lg duration-300 focus-within:border-indigo-500>
      <input
        type="password"
        v-model="confirmPassword"
        placeholder="Password"
        class="w-full border-none bg-transparent outline-none placeholder:italic focus:outline-none"
      />
    </div>

    <button
      class="transform rounded-sm bg-indigo-600 py-2 font-bold duration-300 hover:bg-indigo-400"
    >
      LOG IN
    </button>

    <a
      href="#"
      class="transform text-center font-semibold text-gray-500 duration-300 hover:text-gray-300"
      >FORGOT PASSWORD?</a
    >

    <p class="text-center text-lg">
      No account?
      <a
        href="#"
        class="font-medium text-indigo-500 underline-offset-4 hover:underline"
        >Create One</a
      >
    </p>
  </section>
</main>


  <div>Sign Up</div>
  <PersonalRouter :route="route" :buttonText="buttonText" />
<form @click.prevent="signUp">
    <input type="text" v-model="email">
    <input type="password" v-model="password">
    <input type="password" v-model="confirmPassword">
    <input class="button" type="submit">
  </form>
</template>

<script setup>
import { ref } from "vue";
import { useRouter } from "vue-router";
import { useUserStore } from "../stores/user";

const router = useRouter();
const email = ref("");
const password = ref("");
const confirmPassword = ref("");
const errorMsg = ref(null);

const userStore = useUserStore();

async function signUp() {
  if (password.value === confirmPassword.value) {
    try {
      await userStore.signUp(
        email.value,
        password.value,
        confirmPassword.value
      );
      router.push({ path: "/auth/login" });
    } catch (e) {
      console.log("error");
      errorMsg.value = "Could not sign you up please contact support";
    }
  } else {
    errorMsg.value = "Please enter valid login details";
  }
}
</script>

<style>

</style>