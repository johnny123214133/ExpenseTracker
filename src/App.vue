<template>
	<Header />
	<div class="container">
		<Balance :total="total" /><!-- :total="total" -->
		<IncomeExpenseSummary :income="income" :expenses="expenses" />
		<TransactionList :transactions="transactions" />
		<AddTransaction />

	</div>

</template>

<script setup>
import Header from './components/Header.vue'
import Balance from './components/Balance.vue'
import IncomeExpenseSummary from './components/IncomeExpenseSummary.vue'
import TransactionList from './components/TransactionList.vue'
import AddTransaction from './components/AddTransaction.vue'

import { ref, computed } from 'vue'

const transactions = ref([
	{id: 1, note: 'Flowers', amount: -19.99 },
	{id: 2, note: 'Paycheck', amount: 1032.83 },
	{id: 3, note: 'Book', amount: -27.99 },
	{id: 4, note: 'Cough drops', amount: -7.99 },
])

// get total
const total = computed(() => {
	return transactions.value
		.reduce((acc, transaction) => {
			return acc + transaction.amount
		}, 0)
		.toFixed(2)
})

// get income
const income = computed(() => {
	return transactions.value
		.filter((transaction) => { 
			return transaction.amount >= 0 
		})
		.reduce((acc, transaction) => {
			return acc + transaction.amount
		}, 0)
		.toFixed(2)
})

// get expenses
const expenses = computed(() => {
	return transactions.value
		.filter((transaction) => { 
			return transaction.amount < 0 
		})
		.reduce((acc, transaction) => {
			return acc + transaction.amount
		}, 0)
		.toFixed(2)
})


</script>
