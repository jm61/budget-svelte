<script>
    export let title = 'default title'

</script>
<div class="main-title">
    <h2>{title}</h2>
</div>

<style>
.main-title {
    text-align: center;
    margin-top: 2rem;
    display: grid;
    grid-template-columns: minmax(50px, 1fr) auto minmax(50px, 1fr);
    align-items: center;
    gap: 40px;
}
.main-title::before, .main-title::after {
   content: '';
   border-top: 6px double; 
}
</style>
