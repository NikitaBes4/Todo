<script>
    import { createEventDispatcher } from "svelte";
    const dispatch = createEventDispatcher();

    import { onMount } from "svelte";
    import { supabase } from "./store";
    import { supauser } from "./store";
    let todos = null;
    let newItem = '';
 
    onMount(

        async () => {
            refresh();
        },

    );

    async function refresh() {
        let { data: ToDo, error } = await supabase
            .from("ToDo")
            .select("*");

        if (ToDo) {
            todos = ToDo;
        }
    }

    async function addToList() {
        const { data, error } = await supabase
            .from("ToDo")
            .insert([{User_ID: $supauser.user.id, Text: newItem, Checked: false }])
            .select();
    

        console.log(error, data);
        if (data) {
            todos = [
                ...todos,
                {id:data[0].id, User_Id: data[0].User_ID, Text: data[0].Text, Checked: data[0].Checked },
            ];
        }
    }
    async function Delete(id) {
    const { error } = await supabase
  .from('ToDo')
  .delete()
  .eq('id', id)
  refresh()       
    }

    async function onChange(ev) {
        console.log(ev.srcElement.checked);

        const { data, error } = await supabase
            .from("ToDo")
            .update({ done: ev.srcElement.checked })
            .eq("id", ev.srcElement.id)
            .select();

        console.log(data,error)
     }
</script>
<div class = "text-black">
    {#if todos}
        <div class="flex flex-col">
            {#each todos as item}
                <div class="[&:not(:first-child)]:border-l
                            [&:not(:first-child)]:border-r
                            [&:not(:first-child)]:border-b
                            [&:first-child]:border
                             border-black
                            todorow
                            p-2">
                    
                    <div >
                        {item.id}
                    </div>
                    <div class="check">
                    <div >
                        <input
                            id={item.id}
                            on:change={onChange}
                            bind:checked={item.Done}
                            type="checkbox"  
                        />

                    </div>
                </div>
                    <div style=" text-align:lesft">
                        {item.Text}
                        
                    </div>
                    
                    <div >
                        <button on:click={() => Delete(item.id)}>
                            ❌
                        </button>
                    </div>
                </div>
            {/each}
            
        </div>
    {:else}
        <p>Загрузка данных...</p>
    {/if}

        <input bind:value={newItem} type="text" placeholder="Новое дело..">
        <button on:click={addToList}> Добавить </button>

    <div>
        <button on:click={refresh}> Обновить </button>
    </div>
</div>
<style>
    .todorow{
        display: grid;
        gap: 5px;
        grid-template-columns:  20px 20px 1fr 20px;
        grid-template-rows: 1fr;
        align-items: center;
    }
    .check{
        text-align: center;
    }
</style>
