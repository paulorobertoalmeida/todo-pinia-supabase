<template>
  <!-- component -->
  <!-- page -->
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
    <section
      class="form-sign-in flex w-[30rem] flex-col space-y-10"
      @submit.prevent="signUp"
    >
      <div class="text-center text-4xl font-medium">
        Sign Up - Register to my App
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
          type="email"
          v-model="email"
          required
          placeholder="example@gmail.com"
          class="
            input-field
            w-full
            border-none
            bg-transparent
            outline-none
            placeholder:italic
            focus:outline-none
          "
          id="email"
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
            input-field
            w-full
            border-none
            bg-transparent
            outline-none
            placeholder:italic
            focus:outline-none
          "
        />
      </div>
      <div class="
        w-full
        transform
        border-b-2
        bg-transparent
        text-lg
        duration-300
        focus-within:border-indigo-500"
      >
        <input
          type="password"
          v-model="confirmPassword"
          required
          placeholder="**********"
          class="
            w-full
            border-none
            bg-transparent
            outline-none
            placeholder:italic
            focus:outline-none
          "
        />
      </div>

      <button
        type="submit"
        class="
        button
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

      <p>
        No account?
        <PersonalRouter
          :route="route"
          :buttonText="buttonText"
          class="sign-up-link"
        />
      </p>
    <div v-show="errorMsg">{{errorMsg}}</div>

    </section>
  </main>

  <!-- <div>Sign Up</div>
  <PersonalRouter :route="route" :buttonText="buttonText" />
  <form @click.prevent="signUp">
    <input type="text" v-model="email" />
    <input type="password" v-model="password" />
    <input type="password" v-model="confirmPassword" />
    <input class="button" type="submit" />
  </form> -->
</template>

<script setup>
import { ref, computed } from "vue";
import PersonalRouter from "./PersonalRouter.vue";
import { supabase } from "../supabase";
import { useRouter } from "vue-router";
import { useUserStore } from "@/stores/user";
import { storeToRefs } from "pinia";
// Route Variables
const route = "/auth/login";
const buttonText = "Sign In";
// Input Fields
const email = ref("");
const password = ref("");
const confirmPassword = ref("");
// Error Message
const errorMsg = ref("");
// Show hide password variable
const passwordFieldType = computed(() =>
  hidePassword.value ? "password" : "text"
);
const hidePassword = ref(true);
// Show hide confrimPassword variable
const confirmPasswordFieldType = computed(() =>
  hideConfirmPassword.value ? "password" : "text"
);
const hideConfirmPassword = ref(true);
// Router to push user once SignedUp to Log In
const redirect = useRouter();
// Arrow function to SignUp user to supaBase with a timeOut() method for showing the error
const signUp = async () => {
  if (password.value === confirmPassword.value) {
    try {
      // calls the user store and send the users info to backend to logIn
      await useUserStore().signUp(email.value, password.value);
      // redirects user to the homeView
      redirect.push({ path: "/auth/login" });
    }
    catch (error) {
      // displays error message
      errorMsg.value = error.message;
      // hides error message
      setTimeout(() => {
        errorMsg.value = null;
      }, 5000);
    }
    return;
  }
  errorMsg.value = "Passwords are not the same :(";
};
</script>

<style>
</style>