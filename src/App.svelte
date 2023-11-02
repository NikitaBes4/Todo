<script>
    import TodoApp from "./TodoApp.svelte";
    import Teg from "./teg.svelte"
    
    const components = [
    { comp: 'comp1', component: TodoApp },
    { comp: 'comp2', component: Teg},
];

let selected = components[0];

</script>

<select class="select select-warning w-full max-w-xs" bind:value={selected}>
	{#each components as components}
		<option value={components}>{components.comp}</option>
	{/each}
</select>

<div>
<svelte:component this={selected.component} />
</div>