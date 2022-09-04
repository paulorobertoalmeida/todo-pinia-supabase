<template>
  <div class="bg-black">
    <section>
      <div class="container">
        <h1 class="main-footer">
          <span class="inline md:block">Vue3-Pinia-Supabase</span>
          <span class=""> ToDo<span class="inner-span"> App</span> </span>
        </h1>
      </div>
    </section>

    <hr class="text-white mx-5" />
    <footer class="bg-black pb-5">
      <div class="max-w-screen-xl px-4 pt-8 mx-auto sm:px-6 lg:px-8">
        <div class="sm:flex sm:items-center sm:justify-between">
          <div class="flex justify-center text-teal-300 sm:justify-start"></div>

          <p
            class=""
          >
            Made with tailwind &nbsp; Paulo Almeida &nbsp; Privacy & Policy
            &nbsp; TodoApp
          </p>
        </div>
      </div>
    </footer>
  </div>
</template>

<script setup></script>

<style>
.container {
  @apply: max-w-lg bg-black px-4 pt-24 py-8 mx-auto text-left md: max-w-none md:
    text-center;
}
.main-footer {
  @apply: text-3xl font-extrabold leading-10 tracking-tight text-left text-white
    text-center sm: leading-none md: text-6xl text-4xl lg: text-7xl;
}
span {
  @apply: mt-2 bg-clip-text text-transparent bg-gradient-to-r from-purple-400
    via-emerald-400 to-green-500 md: inline-block;
}
.inner-span {
  @apply: bg-clip-text text-transparent bg-gradient-to-r from-teal-500
    via-cyon-400 to-purple-300;
}
p{
  @apply: mt-4 text-sm text-center text-gray-400 lg:text-right lg:mt-0
}
</style>
