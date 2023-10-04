<script>
    // import { prevent_default } from "svelte/internal";

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

<div class = "flexclass">
	<div>
<h1>Список дел</h1>
<form on:submit|preventDefault={addToList}>
<input bind:value={newItem} type="text" placeholder="new todo item..">
<button disabled={!newItem}>
	Add
</button>
<!-- <button on:click={addToList}>
 Add
</button> -->
</form>

{#each todoList as item, index}

<div class = "table">
<input bind:checked={item.status} type="checkbox">
<div class:checked={item.status}>
	{item.text}
</div>
<div class = "cross" on:click={() => removeFromList(index)}>
	&times;
</div>
</div>

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
  
  .item div:nth-child(2)
  {
  width: 100%;
  }

  .cross
  {
	font-size: 2em;
	color: brown;
  }

</style> 