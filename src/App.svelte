<script>

    import SignIn from './SignIn.svelte';
	import { supauser  } from './store';
	import Form from './form.svelte'

	let comp =null
    
	function toggleComp(){
	    // comp = SignIn
		comp = SignIn //Form
    }
   function hideSignIn(){
	 comp =null
   }



	
</script>

<main>
		
<button on:click={toggleComp}>Comp</button>

		{#if $supauser.user != null }
			<p>x{$supauser.user.id}</p>
		{/if}

		<svelte:component this={comp} hide={hideSignIn}/>


       
 </main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}


	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>