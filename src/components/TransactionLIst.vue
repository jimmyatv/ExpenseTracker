<template>
	<h3>History</h3>
	<ul id="list" class="list">
		<li
			v-for="(transation, idx) in transactions"
			:key="idx"
			:class="transation.amount < 0 ? 'minus' : 'plus'"
		>
			<span>{{ transation.text }}</span> <span>${{ transation.amount }}</span
			><button class="delete-btn">x</button>
		</li>
	</ul>
</template>

//New way to export default directly
<script setup>
	import {defineProps} from 'vue';

    const props = defineProps({
        transactions: {
            type: Array,
            required: true,
        },
    })
</script>

<style>
</style>