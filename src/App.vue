<template>
	<Header />
	<div class="container">
		<Balance />
		<IncomeExpenseSummary />
		<TransactionList />
		<AddTransaction />

	</div>

</template>

<script type="text/javascript">
	import Header from './components/Header.vue'
	import Balance from './components/Balance.vue'
	import IncomeExpenseSummary from './components/IncomeExpenseSummary.vue'
	import TransactionList from './components/TransactionList.vue'
	import AddTransaction from './components/AddTransaction.vue'

	export default {
		components: {
			Header,
			Balance,
			IncomeExpenseSummary,
			TransactionList,
			AddTransaction,
		}
	}
</script>
