<script>
	import {setContext, onMount, afterUpdate} from 'svelte'
	//localStorage.setItem('fuck storage','plein les couilles')
	import Navbar from './components/Navbar.svelte'
	import List from './components/List.svelte'
	import ExpenseForm from './components/ExpenseForm.svelte'
	import Modal from './components/Modal.svelte'
	//import expensesData from '../expenses'
	let expenses = []
	let setName = ''
	let setAmount = null
	let setId = null
	let isFormOpen = false
	$: total = expenses.reduce((acc,i) => acc+=i.amount,0)
	$: isEditing = setId ? true: false

	function removeExpense(id) {
		expenses = expenses.filter( item => item.id !== id)
	}
	function clearExpenses() {
		expenses = []
	}
	function addExpense({name, amount}) {
		let expense = {
			id: Math.floor(Math.random()*1000),
    		name,
    		amount
		}
		expenses = [expense,...expenses]
	}
	function editExpense({name,amount}) {
		expenses = expenses.map(item =>{
			return item.id === setId ? {...item,name,amount} : {...item}
		})
		setId = null
		setAmount = null
		setName = ''
	}
	function setModExp (id) {
		let expense = expenses.find(item => item.id == id)
		setId = expense.id
		setName = expense.name
		setAmount = expense.amount
		showForm()
	}
	function showForm () {
		isFormOpen = true
	}
	function closeForm () {
		isFormOpen = false
		setName = ''
		setAmount = null
		setId = null
	}
	setContext('remove', removeExpense)
	setContext('modify', setModExp)
	// local storage
	function setLocalStorage() {
		localStorage.setItem('expenses',JSON.stringify(expenses))
	}
	onMount(() => {
		expenses = localStorage.getItem('expenses')? JSON.parse(localStorage.getItem('expenses')) :[]
	})
	afterUpdate(() => {
		console.count('after update')
		setLocalStorage()
	})
</script>

<Navbar {total} {showForm} />
<main class="content">
	{#if isFormOpen}
	<Modal>
	<ExpenseForm
		{addExpense}
		name={setName} amount={setAmount} 
		{isEditing}
		{editExpense}
		{closeForm}/>
	</Modal>
	{/if}
	<List {expenses} />
	<button type=button class="btn btn-primary btn-block" on:click={clearExpenses}>clear expenses</button>
</main>





