<script>
	import { supauser } from "./store";
	import Signup from "./Sign_In.svelte";
	import Todo from "./todo.svelte"
	let comp = null;

	function toggleComp() {
		comp = Signup;
	}
	function hideSignIn() {
		comp = null;
	}
</script>


<main
	class="border border-amber-400 flex flex-col align-middle justify-between min-h-screen h-auto p-2 m-2"
>

	<ul class="flex flex-row h-10 content-center flex-wrap px-3 bg-amber-500 text-black">
		<li>
			<button on:click={toggleComp}>Вход</button>
		</li>
		<li>
			<button on:click={() => (comp = null)}>Скрыть</button>
		</li>
		{#if $supauser.user}
		    <li>
			    <button on:click={() => (comp = Todo)}>Список дел</button>
		    </li>
		{/if}
	</ul>


	<div class="w-1/2  bg-amber-500/75 m-auto">
	    <svelte:component this={comp} hide={hideSignIn} class="m-auto " />
    </div>
	<div class=" p-2 bg-amber-500  text-black">
		<p>
			Footer (подвал). Всегда должен быть внизу страницы. Родитель д.б.
			flex-col justify-between
		</p>
	</div>
</main>

<style>
	:global(body) {
		height: 100vh;
		background-color: rgb(207, 170, 115)
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