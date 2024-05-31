<template>
  <Header />

  <div class="container">
    <Balance :total="+total" />
    <Income :income="+income" :expense="-expense" />
    <TransactionList
      :transactions="transactions"
      @transactionDeleted="handleTransactionDeleted"
    />
    <AddTranscation @transactionSubmitted="handleTransactionSubmitted" />
  </div>
</template>

<script setup>
import { ref, computed } from "vue";
import Header from "./components/hedaer.vue";
import Balance from "./components/balance.vue";
import AddTranscation from "./components/addTransaction.vue";
import Income from "./components/incomeExpenses.vue";
import TransactionList from "./components/transaction.vue";
import { useToast } from "vue-toastification";
const toast = useToast();
const transactions = ref([
  { id: 1, name: "John", amount: 100 },
  { id: 2, name: "trex", amount: -100 },
  { id: 3, name: "Max", amount: 500 },
  { id: 4, name: "MAy", amount: -85 },
]);

//get total
const total = computed(() => {
  return transactions.value.reduce((acc, transaction) => {
    return acc + transaction.amount;
  }, 0);
});

//get income
const income = computed(() => {
  return transactions.value
    .filter((transaction) => transaction.amount > 0)
    .reduce((acc, transaction) => {
      return acc + transaction.amount;
    }, 0);
});

//get expenses

const expense = computed(() => {
  return transactions.value
    .filter((transaction) => transaction.amount < 0)
    .reduce((acc, transaction) => {
      return acc + transaction.amount;
    }, 0);
  // .toFixed(2);
});

// add transaction

const handleTransactionSubmitted = (transData) => {
  transactions.value.push({
    id: generateUniqueId(),
    name: transData.name,
    amount: transData.amount,
  });
  con;
  toast.success("transaction added");
};
//generate unique id
const generateUniqueId = () => {
  return Math.floor(Math.random() * 100000000);
};

//delete
const handleTransactionDeleted = (id) => {
  transactions.value = transactions.value.filter(
    (transaction) => transaction.id !== id
  );
  toast.success("transacton deleted");
};
</script> 

<style>
</style>