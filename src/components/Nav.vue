<template>
  <!-- component -->
  <nav
    id="header"
    class="
      w-full
      z-30
      top-10
      py-1
      bg-[#5D4A66]
      shadow-lg
      
      
    "
  >
    <div class="w-full flex items-center justify-between mt-0 px-6 py-2">
      <label for="menu-toggle" class="cursor-pointer md:hidden block">
        <svg
          class="fill-current text-blue-600"
          xmlns="http://www.w3.org/2000/svg"
          width="20"
          height="20"
          viewBox="0 0 20 20"
        >
          <title>menu</title>
          <path d="M0 3h20v2H0V3zm0 6h20v2H0V9zm0 6h20v2H0v-2z"></path>
        </svg>
      </label>
      <input class="hidden" type="checkbox" id="menu-toggle" />

      <div
        class="
          hidden
          md:flex md:items-center md:w-auto
          w-full
          order-3
          md:order-1
        "
        id="menu"
      >
        <nav>
          <ul
            class="
              md:flex
              items-center
              justify-between
              text-base text-white
              pt-4
              md:pt-0
            "
          >
            <li>
              <a
                class="
                  inline-block
                  no-underline
                  hover:text-black
                  font-medium
                  text-lg
                  py-2
                  px-4
                  lg:-ml-2
                "
                href="#"
                >Home</a
              >
            </li>
            <li>
            </li>
            <li>
              <a :to="route" id="signout" class="button-red" @click="signOut">
                <span class="fa fa-info-circle"></span
                ><span class="link"> Sign Out</span></a
              >
            </li>
          </ul>
        </nav>
      </div>

      <div
        class="
          order-2
          md:order-3
          flex flex-wrap
          items-center
          justify-end
          mr-0
          md:mr-4
        "
        id="nav-content"
      >
        <div class="auth flex items-center w-full md:w-full">
          <p p-2>
            Welcome <span class="usuario-name">{{ emailName[0] }}</span>
          </p>
          <button
            @click="signOut"
            class="
              button
              bg-[#3EB642]
              text-gray-200
              p-2
              rounded
              hover:bg-[#579A5D]hover:text-gray-100
              mr-2
            "
          >
            Log Out
          </button>
        </div>
      </div>
    </div>
  </nav>
</template>

<script setup>
// import PersonalRouter from "./PersonalRouter.vue";
import { useUserStore } from "../stores/user";
import { computed } from "vue";
import { useRouter } from "vue-router";
//constant to save a variable that will hold the use router method
const route = "/";
const buttonText = "Todo app";
// constant to save a variable that will get the user from store with a computed function imported from vue
// const getUser = computed(() => useUserStore().user);
const getUser = useUserStore().user;
// constant that calls user email from the useUSerStore
const userEmail = getUser.email;
// constant that saves the user email and cleans out the @client from the user
const emailName = userEmail.split("@");
// async function that calls the signOut method from the useUserStore and pushes the user back to the Auth view.
const redirect = useRouter();
const signOut = async () => {
  try {
    // calls the user store and send the users info to backend to signOut
    await useUserStore().signOut();
    // redirects user to the homeView
    redirect.push({ path: "/auth/login" });
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

<style></style>
