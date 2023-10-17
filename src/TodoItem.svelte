<script>
    export let ItemData
    export let ItemIndex
    export let Remove
</script>

<todoItem class = "">
<div>
<input bind:checked={ItemData.Stats} type="checkbox">
<div class:checked={ItemData.Stats}>
{ItemData.text}
</div>
<div class = "cross" on:click={() => Remove(ItemIndex)}>
&times;
</div>
</div>
</todoItem>

<style> 
	.item div:nth-child(2){
width: 10em ;
display: flex;
flex-direction: row;
align-items: center;
	}
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
	.del {
		font-size: 1.7em;
		color: lawngreen;
	}

.cross
 {
   font-size: 2em;
   color: brown;
 }

 .checked 
  {
    text-decoration: line-through;
  }
</style> 