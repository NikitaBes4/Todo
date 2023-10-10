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

<div>
<div>
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

/>

{/each}

<p>{uncompletedCount} из {allcount} дел выполнено</p>
</div>
</div>

<style>
	.checked 
	{
    text-decoration: line-through;
    }

	.flexclass 
	{
 	display: flex;
 	flex-wrap: wrap;
 	justify-content: center;
 	align-content: center;
 	height: 100vh;	
  	}
</style>