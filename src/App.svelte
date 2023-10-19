<script>
    import TodoItem from "./TodoItem.svelte"
	import todoData from "./Data.js"
	
	let todoList = todoData

    let newItem = "";

	$: uncompletedCount = todoList.filter(t => t.status).length;
	$: allcount = todoList.length;
	
	function addToList() {
		todoList = [...todoList, {text: newItem, status: false}];
		newItem = '';
	}
	function removeFromList(index) {
		todoList.splice(index, 1)
		todoList = todoList;
	}
</script>
	
<div class = "flex1">
<div class = "todo">
	
<h1>Список дел</h1>

<form on:submit|preventDefault={addToList}>
<input bind:value={newItem} type="text" placeholder="new todo item..">
<button disabled={!newItem}>
	Add
</button>
</form>
{#each todoList as item, index}

<TodoItem 
ItemData = {item}
ItemIndex = {index} 
Remove = {removeFromList} 
on:statusCheck = {(event) => {item.status =! item.status}}
/>

{/each}
<p>{uncompletedCount} из {allcount} дел выполнено</p>
</div>
</div>
<style>
	.flex1 
	{
		display: flex;
		height: 100vh;
		justify-content: center;
		align-items: center;
		background: #be6318;
		padding: 4em;
		margin: 1em;
	}
	.todo 
	{
		display: flex;
		flex-direction: column;
		background: #b18422;
		color: rgb(255, 255, 255);
		padding: 4em ;
	}
</style>