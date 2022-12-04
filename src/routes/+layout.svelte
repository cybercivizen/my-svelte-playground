<script lang="ts">
	import '../app.postcss';
	import { Navbar, NavBrand, NavLi, NavUl, NavHamburger } from 'flowbite-svelte';
</script>

<Navbar let:hidden let:toggle navClass="border border-slate-200 rounded-md m-4 p-4  drop-shadow-sm">
	<NavBrand>
      <img src="../src/images/Svelte_Logo.png" alt="Svelte Logo" class="w-4 mr-3 ml-1"/>
		<span class="self-center whitespace-nowrap text-md font-semibold dark:text-white"
			><span class="font-bold text-xl">cybercivizen</span>'s Svelte playground</span
		>
	</NavBrand>
	<NavHamburger on:click={toggle} />
	<NavUl ulClas="text-white" {hidden}>
		<NavLi href="/">Home</NavLi>
		<NavLi href="/todo">Todo List</NavLi>
		<NavLi href="/about">About</NavLi>
	</NavUl>
</Navbar>
<slot />

<style>
   :global(body) {
      background-color:aliceblue
   }
</style>
