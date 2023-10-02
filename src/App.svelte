<script>
    let newItem = '';

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

	function asksStatus() {

    }
</script>
<div class = "flexclass">
	<div>
		<h1>Список дел</h1>
		<input bind:value={newItem} type="text" placeholder="new todo item..">
    <button on:click={addToList}>
		Add
	</button>
		<br/>
		{#each todoList as item, index}
	<span on:click={() => removeFromList(index)}>❌</span>
	<input bind:checked={item.status} type="checkbox">
	<span class:checked={item.status}>{item.text}</span>
	<br/>
{/each} 
<p>{uncompletedCount} из {allcount} дел выполнено</p>
	</div>
</div>

<style> 
	.checked {
    text-decoration: line-through;
    }

	.flexclass {
 	display: flex;
 	flex-wrap: wrap;
 	justify-content: center;
 	align-content: center;
 	height: 100vh;
		
  }
	
</style> 