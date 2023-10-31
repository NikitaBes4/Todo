<script>

import ListToDo from "./DataStore";
import {DataSelect} from "./Data";
import ToDoItem from "./TodoItem.svelte";

let selected = 0;
    

	$: ShowAll = () => {return $ListToDo}
	$: ShowTrue = () => {return $ListToDo.filter(t => t.status == true )}
	$: ShowFalse = () => {return $ListToDo.filter(t => t.status == false )}
	$: funclist = [ShowAll, ShowTrue, ShowFalse]
	
	function removeFromList(event)
	{
		$ListToDo.splice(event.detail.id, 1)
		$ListToDo = $ListToDo;
    }
	
</script>

<fieldset>
	<legend>Фильтрация </legend>

<select
		bind:value={selected}>

		{#each DataSelect as item}
			<option value={item.Id}>
				{item.text}
			</option>
		{/each}
	</select>
	
</fieldset>

{#each funclist[selected]()  as item, index}

	<ToDoItem  
	todoitem = {item} 
	todoIndex = {index} 
	on:ondelete = {removeFromList} 
	on:checkstatus  = {(event) => {item.status = event.detail.stat; $ListToDo = [...$ListToDo]}} 
	/>

{/each} 