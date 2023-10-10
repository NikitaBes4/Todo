<script>

export let ItemData
export let ItemIndex
export let Remove
export let Stats
</script>

<todoItem class = "flexclass">

    <input bind:checked={ItemData.Stats} type="checkbox">
    <div class:checked={ItemData.Stats}>
        {ItemData.text}
    </div>
    <div class = "cross" on:click={() => Remove(ItemIndex)}>
        &times;
    </div>

</todoItem>

<style> 
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