<script>
    import TodoApp from "./TodoApp.svelte";
    import Teg from "./teg.svelte"
    import SignIn from './SignIn.svelte';
	import { supauser  } from './store';
    import { supabase } from "./store";
    import Form from "./form.svelte";
	import Todo from './TodoApp.svelte';
    
	import { onMount } from "svelte";
	export let name;
	
    let data 
	onMount(async () => {
		let n = await supabase.from("Todo").select("User_Id,Checked,Text")
			 console.log('N',n)
        data=n.data
	});
    
let comp =null
function SignInSwitch(){
	    comp = SignIn
    }

    function LogInSwitch(){
	    comp = Form
    }
   function hideSignIn(){
	 comp = null
   }
   function ToDoSwitch(){
	    comp = Todo
    }

</script>
<!-- <button on:click={toggleComp}>Comp</button> -->
 

    <main class="border border-lime-400 flex flex-col h-full p-2 m-2">
	<!-- заготовка для top-меню -->
	<div class = "bg-blue-400">
		<ul class="flex flex-row px-3">
			<li>
				<button on:click={SignInSwitch}>Регистрация</button>
			</li>
			<li>
				<button on:click={() => (comp = null)}>Спрятать</button>
			</li>
            <li>
				<button on:click={LogInSwitch}>Вход</button>
			</li>
			<button on:click={ToDoSwitch}>СписокДел</button>
		</ul>
	</div>

	<!-- контент должен центрироваться по горизонтали и вертикали
	flex-grrow:1 обязательно -->
	<!-- <div class="grow flex flex-col items-center justify-center">
		{#if $supauser.user != null}
			<p>x{$supauser.user.id}</p>
		{/if}
	</div> -->
		<svelte:component this={comp} hide={hideSignIn} />
	

	<!-- margin-top:auto обязательно для фиксации подвала внизу -->
	<div class="mt-auto p-2 bg-slate-200">
		!!!
	</div>
</main>



     <style>
        :global(body) {
		height: 100vh;
		background-color: rgb(235, 245, 245);
        border: 10px solid red;
	    }

        /* main {
            text-align: center;
            padding: 1em;
            max-width: 240px;
            margin: 0 auto;
        } */
    
        @media (min-width: 640px) {
            main {
                background: orange;
            }
        }
    </style>