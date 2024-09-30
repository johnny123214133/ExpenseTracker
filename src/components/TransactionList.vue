<template>
	<h3>History</h3>
	<ul id="list" class="list">
		<!-- v-bind not necessary, :key works too -->
		<li 
			v-for="transaction in transactions" 
			vbind:key=transaction.id 
			:class="transaction.amount < 0 ? 'minus' : 'plus'"
		>
			{{transaction.note}}
			<span v-if="transaction.amount >=0">${{ transaction.amount }}</span>
			<span v-else>-${{ Math.abs(transaction.amount) }}</span>

			<button class="delete-btn" @click="deleteTransaction(transaction.id)">x</button>
		</li>
	
	</ul>
</template>

<script setup>
import { defineProps } from 'vue'

const props = defineProps({
	transactions : {
		type : Array,
		required : true
	}
})

const emit = defineEmits([
	'transactionDeleted'
])

const deleteTransaction = (id) => {
	emit('transactionDeleted', id)
}

</script>