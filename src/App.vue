<template>
	<Header />
	<div class="container">
		<Balance :total="+total" /><!-- :total="total" -->
		<IncomeExpenseSummary :income="+income" :expenses="+expenses" />
		<TransactionList :transactions="transactions" @transactionDeleted="handleTransactionDeleted" />
		<AddTransaction @transactionSubmitted="handleTransactionSubmitted" />

	</div>

</template>

<script setup>
import Header from './components/Header.vue'
import Balance from './components/Balance.vue'
import IncomeExpenseSummary from './components/IncomeExpenseSummary.vue'
import TransactionList from './components/TransactionList.vue'
import AddTransaction from './components/AddTransaction.vue'

import { ref, computed, onMounted } from 'vue'

import { useToast } from 'vue-toastification'

const toast = useToast()

const transactions = ref([])

// const transactions = ref([
// 	{id: 0, note: 'Flowers', amount: -19.99 },
// 	{id: 1, note: 'Paycheck', amount: 1032.83 },
// 	{id: 2, note: 'Book', amount: -27.99 },
// 	{id: 3, note: 'Cough drops', amount: -7.99 },
// ])


onMounted(() => {
	const savedTransactions = JSON.parse(localStorage.getItem('transactions'))
	if (savedTransactions) {
		transactions.value = savedTransactions
	}
})

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

// add transaction
const handleTransactionSubmitted = (transactionData) => {
	transactions.value.push(
		{
			id : Math.floor(Math.random() * 1000000),
			note : transactionData.note,
			amount : transactionData.amount
		}
	)
	saveTransactionsToLocalStorage()
	toast.success('Transaction Added')
}

// delete transaction
const handleTransactionDeleted = (id) => {
	transactions.value = transactions.value.filter((transaction) => {
		return transaction.id !== id
	})
	saveTransactionsToLocalStorage()
	toast.success('Transaction Deleted')
}

// save transactions locally
const saveTransactionsToLocalStorage = () => {
	localStorage.setItem('transactions', JSON.stringify(transactions.value))
}

</script>
