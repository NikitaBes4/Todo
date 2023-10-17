<script>
    import TodoItem from "./TodoItem.svelte"

    let newItem = "";

    let todoList = [{text: 'Write my first post', status: true},
                    {text: 'Upload the post to the blog', status: false},
                    {text: 'Publish the post at Facebook', status: false}];

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

<div class = "todos" on:submit|preventDefault={addToList}>
<input bind:value={newItem} type="text" placeholder="new todo item..">
<button disabled={!newItem}>
	Add
</button>
</div>
{#each todoList as item, index}

<TodoItem 
ItemData = {item}
ItemIndex = {index} 
Remove = {removeFromList} 
/>

{/each}
</div>
</div>
<p>{uncompletedCount} из {allcount} дел выполнено</p>
<style>

	.item {
		display: flex;
		flex-direction: row;
		justify-content: space-between;
		
	}
	.checked {
		text-decoration: line-through;
	}
	.flex1 {
		display: flex;
		height: 100vh;
		justify-content: center;
		align-items: center;
		background: #183544;
		padding: 4em ;
		margin: 4em;
	}
	.todo {
		display: flex;
		flex-direction: column;
		background: #49778f;
		color: whitesmoke;
		padding: 2em ;
	}
	.todos {
		display: flex;
		flex-direction: column;

	}

</style>