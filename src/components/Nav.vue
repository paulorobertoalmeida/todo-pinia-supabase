<template>
 <nav class="relative select-none bg-grey lg:flex lg:items-stretch w-full">
  <div class="flex flex-no-shrink items-stretch h-12">
    <a href="#" class="flex-no-grow flex-no-shrink relative py-2 px-4 leading-normal text-white no-underline flex items-center hover:bg-grey-dark">Tailwind</a>
    <a href="#" class="flex-no-grow flex-no-shrink relative py-2 px-4 leading-normal text-white no-underline flex items-center hover:bg-grey-dark">Css</a>
    <button class="block lg:hidden cursor-pointer ml-auto relative w-12 h-12 p-4">
      <svg class="fill-current text-white" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20"><path d="M0 3h20v2H0V3zm0 6h20v2H0V9zm0 6h20v2H0v-2z"/></svg>
      <svg class="fill-current text-white" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20"><path d="M10 8.586L2.929 1.515 1.515 2.929 8.586 10l-7.071 7.071 1.414 1.414L10 11.414l7.071 7.071 1.414-1.414L11.414 10l7.071-7.071-1.414-1.414L10 8.586z"/></svg>
    </button>
  </div>
  <div class="lg:flex lg:items-stretch lg:flex-no-shrink lg:flex-grow">
    <div class="lg:flex lg:items-stretch lg:justify-end ml-auto">
      <a href="#" class="flex-no-grow flex-no-shrink relative py-2 px-4 leading-normal text-white no-underline flex items-center hover:bg-grey-dark">Item 1</a>
    </div>
  </div>
</nav>
<div id="font-colors">
	Font
	<button id="white" class="btn"></button>
	<button id="black" class="btn"></button>
</div>
<div id="edges">
	Edges
	<button id="rounded" class="btn">Rounded</button>
	<button id="square" class="btn">Square</button>
</div>
<h1>Minimal Bootstrap Navbar</h1>
<nav class="navbar">
	<div class="container-fluid">
		<!-- Nav Header -->
		<div class="navbar-header">
			<button type="button" class="navbar-toggle" data-toggle="collapse" data-target="#collapse-1" aria-expanded="false">
				<span class="icon-bar"></span>
				<span class="icon-bar"></span>
				<span class="icon-bar"></span>
			</button>
			<a class="navbar-brand" href="#"><span class="fa fa-home"></span><span class="link"> Home</span></a>
		</div>
		<!-- Nav Collapse -->
		<div class="navbar-collapse collapse" id="collapse-1">
			<!-- Nav Left -->
			<ul class="nav navbar-nav">
				<!-- Products -->
				<li class="dropdown">
					<a href="#" class="dropdown-toggle" data-toggle="dropdown" role="button" aria-haspopup="true" aria-expanded="false">
						<span class="fa fa-tags"></span><span class="link"> Products</span> <span class="fa fa-caret-down"></span></a>
					<ul class="dropdown-menu">
						<li><a href="#"><span class="fa fa-tag"></span> Catalogue 1</a></li>
						<li><a href="#"><span class="fa fa-tag"></span> Catalogue 2</a></li>
					</ul>
				</li>
				<!-- Services -->
				<li class="dropdown">
					<a href="#" class="dropdown-toggle" data-toggle="dropdown" role="button" aria-haspopup="true" aria-expanded="false">
						<span class="fa fa-gears"></span><span class="link"> Services</span> <span class="fa fa-caret-down"></span></a>
					<ul class="dropdown-menu">
						<li><a href="#"><span class="fa fa-gear"/></span> Service 1</a></li>
						<li><a href="#"><span class="fa fa-gear"/></span> Service 2</a></li>
						<li><a href="#"><span class="fa fa-gear"/></span> Service 3</a></li>
					</ul>
				</li>
				<!-- About -->
				<li><a href="#"><span class="fa fa-info-circle"></span><span class="link"> About</span></a></li>
				<!-- Contact -->
				<li><a href="#"><span class="fa fa-phone"></span><span class="link"> Contact</span></a></li>
			</ul>
			<!-- Nav Right -->
			<form class="navbar-form navbar-right">
				<div class="form-group">
					<input type="text" class="form-control" placeholder="Search">
				</div>
				<button type="submit" class="btn"><span class="fa fa-search"></span></button>
			</form>
		</div>
	</div>
</nav>
<h1>hello</h1>
</template>

<script setup>
//constant to save a variable that will hold the use router method
import { useRouter } from "vue-router";

// constant to save a variable that will get the user from store with a computed function imported from vue

import { useUserStore } from "../store/user.js";
// constant that calls user email from the useUSerStore
const router = useRouter();
const userStore = useUserStore();

async function signOut() {
  try {
    router.push({ path: "/auth" });
    userStore.signOut();
  } catch (e) {
    alert(e);
  }
}






// constant that saves the user email and cleans out the @client from the user

// async function that calls the signOut method from the useUserStore and pushes the user back to the Auth view.
</script>

<style></style>
