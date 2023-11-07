<script>

    import SignIn from './SignIn.svelte';
	import { supauser  } from './store';

	let comp =null
    
	function toggleComp(){
	    comp = SignIn
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

	/* h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	} */

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>