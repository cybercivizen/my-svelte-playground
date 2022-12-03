<script lang="ts"> 
	import '../app.postcss';
   import { Navbar, NavBrand, NavLi, NavUl, NavHamburger } from 'flowbite-svelte'
</script>
<Navbar let:hidden let:toggle navClass="border border-slate-300 rounded-md m-4 px-4  drop-shadow-lg">
   <NavBrand>

      <span class="self-center whitespace-nowrap text-md font-semibold dark:text-white"><span class="font-bold text-xl">cybercivizen</span>'s Svelte playground</span>
   </NavBrand>
   <NavHamburger on:click={toggle}/>
   <NavUl ulClas="text-white" hidden={hidden}>
      <NavLi href='/'>Home</NavLi>
      <NavLi href='/todo'>Todo List</NavLi>
      <NavLi href='/about'>About</NavLi>
   </NavUl>
</Navbar>
<slot />
