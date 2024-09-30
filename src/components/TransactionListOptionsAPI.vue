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
			<span>${{transaction.amount}}</span>
			<button class="delete-btn">x</button>
		</li>
		<li class="minus">
			Cash <span>-$400</span><button class="delete-btn">x</button>
		</li>
		<li class="plus">
			Paycheck <span>$600</span><button class="delete-btn">x</button>
		</li>
	
	</ul>
</template>

<script>
	//Options API
	export default {
		data() {
			return {
				transactions : [
					{id : 1, text : 'Flowers', amount : -19.99 },
					{id : 2, text : 'Paycheck', amount : 1032.83 },
					{id : 3, text : 'Book', amount : -27.99 },
					{id : 4, text : 'Cough drops', amount : -7.99 },
				]
			}//,
			//if defining methods too
			// methods : {

			// }
		}
	}
</script>