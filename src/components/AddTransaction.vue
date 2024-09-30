<template>
	<h3>Add new transaction</h3>
	<form id="form" @submit.prevent="onSubmit">
		<div class="form-control">
			<label for="text">Note</label>
			<input type="text" id="text" v-model="note" placeholder="Enter text..." />
		</div>
		<div class="form-control">
			<label for="amount"
				>Amount <br />
				(negative : expense, 
				positive : income)</label
			>
			<input type="text" id="amount" v-model="amount" placeholder="Enter amount..." />
		</div>
		<button class="btn">Add transaction</button>
	</form>
</template>

<script setup>
import { ref } from 'vue'
import { useToast } from 'vue-toastification'

const note = ref('')
const amount = ref('')

const toast = useToast()

const emit = defineEmits([
	'transactionSubmitted'
])

const onSubmit = () => {
	if (!note.value || !amount.value) {
		toast.error('Note and Amount fields must be filled')
		return
	}
	if (isNaN(Number(amount.value))) {
		toast.error('Amount must be a number')
		return
	}

	console.log('submit')
	console.log(note.value, amount.value)

	const transactionData = {
		note : note.value,
		amount : Number(Number(amount.value).toFixed(2))
	}
	
	emit('transactionSubmitted', transactionData)

	note.value = ''
	amount.value = ''
}
</script>