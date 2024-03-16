<template>
	<Header />
	<div class="container">
		<Balance :total='total' />
		<IncomeExpenses :income='+income' :expenses='+expenses' />
		<TransactionLIst :transactions='transactions' @transactionDeleted="handleTransactionDeleted" />
		<AddTransaction @transactionSubmitted='handleTransactionSubmitted' />
	</div>
</template>

<script setup>
	import { ref, computed } from "vue";
	import { useToast } from "vue-toastification";

	import AddTransaction from "./components/AddTransaction.vue";
	import Balance from "./components/Balance.vue";
	import Header from "./components/Header.vue";
	import IncomeExpenses from "./components/IncomeExpenses.vue";
	import TransactionLIst from "./components/TransactionLIst.vue";

  const toast = useToast();

	const transactions = ref([
		{ id: "1", text: "Flower", amount: -19.99 },
		{ id: "2", text: "Salary", amount: 299.99 },
		{ id: "3", text: "Book", amount: -15 },
		{ id: "4", text: "Camera", amount: 150 },
	]);

// Get total
  const total = computed(() => {
    return transactions.value.reduce((acc, transaction) => {
      return acc + transaction.amount;
    }, 0)
  });

  //Get income
const income = computed(() => {
    return transactions.value
    .filter((transaction) => transaction.amount > 0)
    .reduce((acc, transaction) => {
      return acc + transaction.amount;
    }, 0).toFixed(2);
  });

  //Get expenses
  const expenses = computed(() => {
    return transactions.value
    .filter((transaction) => transaction.amount < 0)
    .reduce((acc, transaction) => {
      return acc + transaction.amount;
    }, 0).toFixed(2);
  });

  //Add transactions
  const handleTransactionSubmitted = (transactionData) => {
    transactions.value.push({
      id: generateUniqueId(),
      text: transactionData.text,
      amount: transactionData.amount
    });

    toast.success('Transaction added')
  };

  //Generate Unique Id 
  const generateUniqueId = () => {
    return Math.floor(Math.random() * 1000000)
  }

  //Delete transaction
  const handleTransactionDeleted = (id) => {
    transactions.value = transactions.value.filter((transaction) => 
    transaction.id != id);

    toast.success('Transaction deleted')
  }
</script>

<style>
</style>