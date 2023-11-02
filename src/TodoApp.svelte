<script>
    import Info from "./InfoToDoList.svelte";
    import AddToDoList from "./AddToDoList.svelte";
	import FilterSelect from "./FilterSelect.svelte"
	import { supabase } from "./store";
	import { onMount } from "svelte";

	let data 

	onMount(async () => {
		let n = await supabase
             .from('countries')
             .select('id,name')
			 console.log('N',n)
        data=n.data
	});
</script>

<div class = "flex" >
<div>

<AddToDoList />
<FilterSelect />
<Info />

</div>
</div>

<style> 

	.flex
	{
			display: flex;
			justify-content: center;
			flex-wrap: wrap;
		  	align-content: center;
			height: 100vh;
			background: rgb(223, 108, 0);
			color: white;
			
	}

</style> 