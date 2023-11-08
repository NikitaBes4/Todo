<script>
    import TodoApp from "./TodoApp.svelte";
    import Teg from "./teg.svelte"
    import SignIn from './SignIn.svelte';
	import { supauser  } from './store';
    import { supabase } from "./store";

    
	import { onMount } from "svelte";
	export let name;
	
    let data 
	onMount(async () => {
		let n = await supabase.from("Todo").select("User_Id,Checked,Text")
			 console.log('N',n)
        data=n.data
	});
    
let comp =null
function toggleComp(){
	    comp = SignIn
    }
   function hideSignIn(){
	 comp =null
   }

</script>
<button on:click={toggleComp}>Comp</button>
 
<main>
{#if data}

    {#each data  as item}
    <div style='display:flex; flex-direction:row'>
    <p>{item.User_Id}</p>
    <p>{item.Checked}</p>
    <p>{item.Text}</p>
     </div>
    {/each}
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