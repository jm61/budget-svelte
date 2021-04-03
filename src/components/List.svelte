<script>
    import Title from './Title.svelte'
    import Expense from './Expense.svelte'
    import {fly} from 'svelte/transition'
    import {flip} from 'svelte/animate'
    export let expenses = []
</script>

<section>
    <Title title="expenses list" />
    <ul>
        {#each expenses as expense,idx (expense.id)}
            <div transition:fly={{x:-400,delay:500*idx}} animate:flip>
                <Expense {...expense} />
            </div>
            {:else}
            <h2><mark>No expenses yet...</mark></h2>
        {/each}
    </ul>
</section>
