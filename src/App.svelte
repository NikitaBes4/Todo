<script>
let EvenNum = [1, 2, 3, 4, 5, 6]
function AddNum()
	{
			EvenNum = [...EvenNum, EvenNum.length + 1]	
	}

function DelNum(i)
{
	EvenNum = EvenNum.filter((e,i)=> i != i)
}

</script>

<button on:click={AddNum}>
	<h1>AddNumer</h1>
</button>
<p>{EvenNum}</p>
<div>
	{#each EvenNum as num}
		{#if num%2 == 0 && num < 10}
		<p>{num}</p>
		{/if}
		{#if num%2 == 0 && num%2 == 0}
		<p class = "bgcolor">{num} </p>
	  {/if}
	{/each}
</div>

<div>
	
    {#each EvenNum as num, i}
	<button
	on:click = {() => DelNum(i)}>
		{i + 1}</button>

	{/each}

</div>
	
<style>
	.bgcolor{background:blue;}
</style>