<script>
    
   import Title from './Title.svelte'
   export let name = ''
   export let amount = null
   export let addExpense
   export let editExpense
   export let isEditing
   export let closeForm
   $: isEmpty = !name || !amount

   function handleSubmit() {
    if(isEditing){
        editExpense({name,amount})
    } else {
        addExpense({name, amount})
    }
    name = ''
    amount = null
    closeForm()
   }
</script>
<section class="form">
    {#if isEditing}
    <Title title="edit expense"/>
    {:else}
    <Title title="add expense"/>
    {/if}
    <form class="expense-form" on:submit|preventDefault={handleSubmit}>
       <div class="form-control">
           <label for="name">name
               <input type="text" id="name" bind:value={name} placeholder="enter your expense..." required>
           </label>
       </div> 
       <div class="form-control">
           <label for="amount">amount
               <input type="number" id="amount" step="10" min="0" bind:value={amount}
               placeholder="enter the amount..." required>
           </label>
       </div>
       {#if isEmpty}
       <p class="form-empty">please fill out all fields</p>
       {/if}
       <button id="btn" type="submit" class="btn btn-block" class:disabled={isEmpty} disabled={isEmpty}>
        {#if isEditing}
            save edit expense
        {:else}
            add expense
        {/if}</button>
       <button type=button class="close-btn" on:click={closeForm}><i class="fas fa-times"></i></button>
    </form>
</section>

<style>

</style>