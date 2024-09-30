<template>
	<h3>History</h3>
	<ul id="list" class="list">
		<!-- v-bind not necessary, :key works too -->
		<li 
			v-for="transaction in transactions" 
			vbind:key=transaction.id 
			:class="transaction.amount < 0 ? 'minus' : 'plus'"
		>
			{{transaction.text}}
			<span v-if="transaction.amount >=0">${{ transaction.amount }}</span>
			<span v-else>-${{ Math.abs(transaction.amount) }}</span>

			<button class="delete-btn">x</button>
		</li>
	
	</ul>
</template>

<script setup>
	//Composition API

	const transactions = [
		{id : 1, text : 'Flowers', amount : -19.99 },
		{id : 2, text : 'Paycheck', amount : 1032.83 },
		{id : 3, text : 'Book', amount : -27.99 },
		{id : 4, text : 'Cough drops', amount : -7.99 },
	]

</script>
<!-- <script>
	//Composition API
	export default {
		setup() {
			const transactions = [
				{id : 1, text : 'Flowers', amount : -19.99 },
				{id : 2, text : 'Paycheck', amount : 1032.83 },
				{id : 3, text : 'Book', amount : -27.99 },
				{id : 4, text : 'Cough drops', amount : -7.99 },
			]

			// objects and methods
			return { 
				transactions
			}
		}
	}
</script> -->