<script>
let EvenNum = []
let src = 'https://upload.wikimedia.org/wikipedia/ru/6/61/Rickrolling.gif';
let name = 'Rick Astley';
function AddNum()
	{
			EvenNum = [...EvenNum, EvenNum.length + 1]	
	}

function DelNum(idx)
{
	EvenNum = EvenNum.filter((e,i)=> idx != i)
}

$:  border = EvenNum.length
</script>

<button on:click={AddNum}>
	<h1>AddNumer</h1>
</button>

<p>{EvenNum}</p>
<div style = {`border:${border}px solid gray`}>
	{#each EvenNum as num}
	 {#if num%3 == 0 && num%3 == 0}
	 <p class = "red">{num} </p>
		{/if}
		{#if num%2 == 0 && num%2 == 0}
	<p class = "blue">{num} </p>
	  {/if}
	{:else}
	<img {src} alt="{name} dances." />
	{/each} 
</div>

<div>
	
    {#each EvenNum as num, i}
	<button
	on:click = {() => DelNum(i)}>
		{num}</button>

	{/each}

</div>
	
<style>
	.even{background:blue;}
	.odd{background:red;}
</style>