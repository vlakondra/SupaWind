<script>
	// import SignIn from "./SignIn.svelte";
	// import SignUp from "./Signup.svelte";

	import Form from "./form.svelte";

	import { supauser } from "./store";
	import Signup from "./Sign_In.svelte";
	import Todo from "./todo.svelte";
	import Chart from "./chartjs.svelte";
	import FusionChrt  from './fusionchart.svelte'
	import CakeChrt from './cake.svelte'
	import Ggb1 from './ggb1.svelte'

	let comp = null;

	function toggleComp(ev) {
		switch (ev.target.id) {
			case 'ggb':
				comp = Ggb1;
				break
			case "signup":
				comp = Signup;
				break;

			case "plot": 
				comp = Chart;
				break;

			case "fusion": 
				comp = FusionChrt;
				break;	

				case "cake": 
				comp = CakeChrt;
				break;	


			default:
				comp = null;
				break;
		}

	}
	function hideSignIn() {
		comp = null;
	}
</script>

<svelte:head>
  <script type="text/javascript" src="https://cdn.geogebra.org/apps/deployggb.js"></script>
</svelte:head>

<main
	class="border border-gray-400 flex flex-col align-middle justify-between min-h-screen h-auto p-2 m-2"
>

<!-- <main class="border border-gray-400 flex container min-h-screen h-auto p-2 m-2"> -->
	
	<!-- заготовка для top-меню -->

	<ul class="flex flex-row h-10 content-center flex-wrap px-3 bg-cyan-500">
		<li>
			<button id="ggb" on:click={toggleComp}>GeoGebra</button>
		</li>
		<li>
			<button id="signup" on:click={toggleComp}>Вход</button>
		</li>
		<li>
			<button id="plot" on:click={toggleComp}>ChartJS</button>
		</li>

		<li>
			<button id="fusion" on:click={toggleComp}>Fusion</button>
		</li>

		<li>
			<button id="cake" on:click={toggleComp}>LayerCake</button>
		</li>


		<li>
			<button on:click={() => (comp = null)}>Hide</button>
		</li>
		{#if $supauser.user}
			<li>
				<button on:click={() => (comp = Todo)}>Список дел</button>
			</li>
		{/if}
	</ul>

	<!-- <div class="flex flex-col items-center justify-center">
		
		{#if $supauser.user != null}
			<p>x{$supauser.user.id}</p>
		{/if}
	</div> -->
	<!-- tmp для проверки центрирования -->
	<!-- <p class="self-center">middle tmp</p> -->

	<!-- место для компонентов -->
	<div class="w-1/2 m-auto">
		<svelte:component this={comp} hide={hideSignIn} />
	</div>

	<div class=" p-2 bg-blue-300">
		<p>
			Footer (подвал). Всегда должен быть внизу страницы. Родитель д.б.
			flex-col justify-between
		</p>
	</div>
</main>

<style>
	:global(body) {
		min-height: 100vh;
		background-color: rgb(228, 238, 238);
	}

	.container {
		display: grid;
		grid-template-rows: auto 1fr auto;
		grid-template-columns: 100%;
	}

	/* навигацию сделать компонентом */
	ul.flex li {
		margin-left: 1rem;
	}

	@media (max-width: 640px) {
		main {
			background-color: bisque;
		}
	}
</style>
