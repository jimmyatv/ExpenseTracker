<template>
	<Header />
	<div class="container">
		<Balance :total='total' />
		<IncomeExpenses />
		<TransactionLIst :transactions='transactions' />
		<AddTransaction />
	</div>
</template>

<script setup>
	import { ref, computed } from "vue";
	import AddTransaction from "./components/AddTransaction.vue";
	import Balance from "./components/Balance.vue";
	import Header from "./components/Header.vue";
	import IncomeExpenses from "./components/IncomeExpenses.vue";
	import TransactionLIst from "./components/TransactionLIst.vue";

	const transactions = ref([
		{ id: "1", text: "Flower", amount: -19.99 },
		{ id: "2", text: "Salary", amount: 299.99 },
		{ id: "3", text: "Book", amount: -10 },
		{ id: "4", text: "Camera", amount: 150 },
	]);

  const total = computed(() => {
    return transactions.value.reduce((acc, transactions) => {
      return acc + transactions.amount
    })
  });
</script>

<style>
</style>