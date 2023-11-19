<script>
	import SignIn from "./SignIn.svelte";
	import SignUp from "./Signup.svelte";
	import { supauser } from "./store";
	import Form from "./form.svelte";
	import Signup from "./Signup.svelte";

	let comp = null;

	function toggleComp() {
		comp = Signup; //SignIn //Form
	}
	function hideSignIn() {
		comp = null;
	}
</script>

<!-- main должен занимать все свободное простр-во: h-full -->
<main class="border border-lime-400 flex flex-col h-full p-2 m-2">
	<div>
		<ul class="flex flex-row px-3">
			<li>
				<button on:click={toggleComp}>SignUp</button>
			</li>
			<li>
				<button on:click={() => (comp = null)}>Hide</button>
			</li>
		</ul>
	</div>
	<div class="grow flex flex-col items-center justify-center">
		{#if $supauser.user != null}
			<p>x{$supauser.user.id}</p>
		{/if}
		<p>middle</p>
		<svelte:component this={comp} hide={hideSignIn} />
	</div>
	<div style="margin-top: auto;"  class=" p-2 bg-slate-200">
		<p>
			Footer (подвал). Всегда должен быть внизу страницы. Как сделать?
			Добавить class="mt-auto". Родитель д.б. flex-col
		</p>
	</div>
</main>

<style>
	:global(body) {
		height: 100vh;
		background-color: rgb(235, 245, 245);
	}



	ul.flex li {
		margin-left: 1rem;
	}
 
	 @media (max-width: 640px) {
		main {
			max-width: none;
			background-color: bisque;
		}
	} 
</style>
