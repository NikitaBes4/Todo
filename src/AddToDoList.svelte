<script>
    import ListToDo from "./DataStore";

    let newItem = "";

    function addToList()
	{
		$ListToDo = [...$ListToDo, {text: newItem, status: false}];
		newItem = '';
	}

</script>

<h1> Список дел </h1>

<input class="input input-bordered input-warning max-w-xs"  bind:value={newItem} type="text" placeholder="new todo item..">
<button class="tooltip btn btn-active btn-accent" data-tip="Добавление" 
 on:click={addToList} disabled={!newItem}>
    Add
</button>
