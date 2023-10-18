<script>
    export let ItemData
    export let ItemIndex
    export let Remove
</script>

<todoItem class = "todo">
<div class = "item">
<input bind:checked={ItemData.Stats} type="checkbox">
<div class:checked={ItemData.Stats}>
{ItemData.text}
<div class = "cross" on:click={() => Remove(ItemIndex)}>
&times;
</div>
</div>

</div>
</todoItem>

<style> 
	.item div:nth-child(2)
	{
		width: 10em ;
		display: flex;
		flex-direction: row;
		align-items: center;
	}
	.item 
	{
		display: flex;
		flex-direction: row;
		justify-content: space-between;
		
	}
	.checked {
		text-decoration: line-through;
	}
	.todo 
	{
		display: flex;
		flex-direction: column;
		background: #b18422;
		color: rgb(255, 255, 255);
		padding: 2em ;
	}
    .cross
    {
   		font-size: 2em;
   		color: red;
    }

    .checked 
    {
    	text-decoration: line-through;
    }
</style> 