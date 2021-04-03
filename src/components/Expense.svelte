<script>
  import {slide} from 'svelte/transition'
  import {getContext} from 'svelte'
  export let id, amount, name;
  let displayAmount = false

  const removeExpense = getContext('remove')
  const setModExp = getContext('modify')
</script>

<article class="single-expense">
  <div class="expense-info">
    <h2>
      {name}<button class="amount-btn" on:click={()=> displayAmount = !displayAmount}>
        <i class="fas fa-caret-down" />
      </button>
    </h2>
    {#if displayAmount}
    <h4 transition:slide>amount: €{amount}</h4>
    {/if}
  </div>
  

  <div class="expense-buttons"><span><small>{id}</small></span>
    <button class="expense-btn edit-btn" on:click={() => setModExp(id)}>
        <i class="fas fa-pen"></i>
    </button>
    <button class="expense-btn delete-btn" on:click={() => removeExpense(id)}>
        <i class="fas fa-trash"></i>
    </button>
  </div>
</article>

<style>
    h4{
        color: slateblue;
        font-weight: 400;
    }
</style>