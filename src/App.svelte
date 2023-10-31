<script>
    import Info from "./InfoToDoList.svelte";
    import AddToDoList from "./AddToDoList.svelte";
	import FilterSelect from "./FilterSelect.svelte"
</script>

<div class = "flex" >
<div>

<AddToDoList />
<FilterSelect />
<Info />

</div>
</div>

<style> 

	.flex{
			display: flex;
			justify-content: center;
			flex-wrap: wrap;
		  	align-content: center;
			height: 100vh;
			background: rgb(223, 108, 0);
			color: white;
			
	}
	
</style> 