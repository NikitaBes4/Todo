<script>
    import TodoApp from "./TodoApp.svelte";
    import Teg from "./teg.svelte"
    import SignIn from './SignIn.svelte';
	import { supauser  } from './store';
    import { supabase } from "./store";
    import Form from "./form.svelte";
    
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
	 comp =null
   }

</script>
<!-- <button on:click={toggleComp}>Comp</button> -->
 

    <main class="border border-lime-400 flex flex-col h-full p-2 m-2">
	<!-- заготовка для top-меню -->
	<div class = "bg-blue-400">
		<ul class="flex flex-row px-3">
			<li>
				<button on:click={SignInSwitch}>SignIn</button>
			</li>
			<li>
				<button on:click={() => (comp = null)}>Hide</button>
			</li>
            <li>
				<button on:click={LogInSwitch}>Login</button>
			</li>
		</ul>
	</div>

	<!-- контент должен центрироваться по горизонтали и вертикали
	flex-grrow:1 обязательно -->
	<div class="grow flex flex-col items-center justify-center">
		<!-- tmp для отладки -->
		{#if $supauser.user != null}
			<p>x{$supauser.user.id}</p>
		{/if}
		<!-- tmp для проверки центрирования -->
		<!-- <p>middle tmp</p> -->
		<!-- место для компонентов -->
		<svelte:component this={comp} hide={hideSignIn} />
	</div>

	<!-- margin-top:auto обязательно для фиксации подвала внизу -->
	<div class="mt-auto p-2 bg-slate-200">
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