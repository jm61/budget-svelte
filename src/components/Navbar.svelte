<script>
let date = new Date().toLocaleDateString('fr',{
    weekday: 'long',
    year: 'numeric',
    month: 'long',
    day: 'numeric'
    })
export let total = 0
export let showForm
</script>

<nav class="nav">
    <div class="nav-center">
        <h1 class="nav-title">Budget Calc</h1>
    <button class="nav-btn" on:click={showForm}>
        <i class="far fa-plus-square"></i> add expense</button>
        <span class="nav-title">{date}</span>
        <span class="nav-title" id=total>Total: €{total}</span>
    </div>
</nav>

<style>
    #total {
        border: 2px solid var(--offWhite);
        padding: .25rem .5rem;
        border-radius: 7px 0;
    }
    .nav-btn {
        color: var(--offWhite);
    }
</style>