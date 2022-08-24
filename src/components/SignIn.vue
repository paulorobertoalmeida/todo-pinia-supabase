<template>
  <main
    class="
      mx-auto
      flex
      min-h-screen
      w-full
      items-center
      justify-center
      bg-gray-900
      text-white
    "
  >
    <!-- component -->
    <form
      class="flex w-[30rem] flex-col space-y-10 form-sign-in"
      @submit.prevent="signIn"
    >
      <div class="text-center text-4xl font-medium">Sign In</div>

      <PersonalRouter :route="route" :buttonText="buttonText" />
      <div
        class="
          w-full
          transform
          border-b-2
          bg-transparent
          text-lg
          duration-300
          focus-within:border-indigo-500
        "
      >
        <p class="">nenoxvx@icloud.com</p>
        <input
          type="email"
          placeholder="example@gmail.com"
          class="
            w-full
            border-none
            bg-transparent
            outline-none
            placeholder:italic
            focus:outline-none
            input-field
          "
          id="email"
          v-model="email"
          required
        />
      </div>

      <div
        class="
          w-full
          transform
          border-b-2
          bg-transparent
          text-lg
          duration-300
          focus-within:border-indigo-500
        "
      >
        <input
          type="password"
          v-model="password" 
          required
          placeholder="**********"
          class="
            w-full
            border-none
            bg-transparent
            outline-none
            placeholder:italic
            focus:outline-none
            input-field
          "
          id="password"
          
        />
      </div>

      <button
        type="submit"
        class="
          transform
          rounded-sm
          bg-indigo-600
          py-2
          font-bold
          duration-300
          hover:bg-indigo-400
        "
      >
        LOG IN
      </button>
      <p>
        Did you have an account?
        <PersonalRouter
          :route="route"
          :buttonText="buttonText"
          class="sign-up-link"
        />
      </p>

      <a
        href="#"
        class="
          transform
          text-center
          font-semibold
          text-gray-500
          duration-300
          hover:text-gray-300
        "
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
    </form>
  </main>

  <!-- <div>Sign In</div>

  <form action="">
    <input :type="text" />
    <input type="text" />
    <input class="button" type="submit" />
  </form> -->
</template>

<script setup>
import { ref, computed } from "vue";
import PersonalRouter from "./PersonalRouter.vue";
import { supabase } from "../supabase";
import { useRouter } from "vue-router";
import { useUserStore } from "../stores/user";
import { storeToRefs } from "pinia";
// Route Variables
const route = "/auth/sign-up";
const buttonText = "Sign Up";
// Input Fields
const email = ref("");
const password = ref("");
// Error Message
const errorMsg = ref("");
//Show hide password variables
const passwordFieldType = computed(() =>
  hidePassword.value ? "password" : "text"
);
const hidePassword = ref(true);
// Router to push user once SignedIn to the HomeView
const redirect = useRouter();
// Arrow function to Signin user to supaBase
const signIn = async () => {
  try {
    // calls the user store and send the users info to backend to logIn
    await useUserStore().signIn(email.value, password.value);
    // redirects user to the homeView
    redirect.push({ path: "/" });
  } catch (error) {
    // displays error message
    errorMsg.value = `Error: ${error.message}`;
    // hides error message
    setTimeout(() => {
      errorMsg.value = null;
    }, 5000);
  }
};
</script>

<style>
</style>