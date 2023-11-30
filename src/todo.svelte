<script>
    import { createEventDispatcher } from "svelte";
    const dispatch = createEventDispatcher();

    import { onMount } from "svelte";
    import { supabase } from "./store";
    import { supauser } from "./store";
    let todos = null;
 
    onMount(
        //Обработка создания компонента
        async () => {
            refresh();
        },
        // async () => {
        // let { data: mytodos, error } = await supabase
        //     .from("mytodos")
        //     .select("*");

        // if (mytodos) {
        //     todos = mytodos;
        // }
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
            .insert([{User_ID: $supauser.user.id, Text: "новое дело 6", Checked: false }])
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

<div class="flex flex-col items-center justify-center text-black">
    {#if todos}
        <div class="flex flex-col">
            {#each todos as item}
                <div class="flex flex-row justify-between">
                    <div>
                        {item.id}
                    </div>
                    <div>
                        <input
                            id={item.id}
                            on:change={onChange}
                            bind:checked={item.Done}
                            type="checkbox"
                        />
                    </div>
                    <div>
                        {item.Text}
                        <button on:click={() => Delete(item.id)}>❌</button>
                    </div>
                </div>
            {/each}
        </div>
    {:else}
        <p>Загрузка данных...</p>
    {/if}

    <div>
        <button on:click={addToList}> Добавить </button>
    </div>
    <div>
        <button on:click={refresh}> Обновить </button>
    </div>
</div>