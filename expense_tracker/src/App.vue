<template>
  <Header />
  <Balance :total="total" />
  <IncomeExpence :income="income" :expenes="expenes" />
  <TransactionList :transactions="transactions" />
  <AddTrasaction />
</template>
<script setup>
import { ref, computed } from "vue";
import Header from "./components/Header.vue";
import Balance from "./components/Balance.vue";
import IncomeExpence from "./components/IncomeExpence.vue";
import TransactionList from "./components/TransactionList.vue";
import AddTrasaction from "./components/AddTrasaction.vue";

const transactions = ref([
  { id: 1, text: "flower", amount: -19 },
  { id: 2, text: "salary", amount: 299 },
  { id: 3, text: "Book", amount: -34 },
  { id: 4, text: "camera", amount: 140 },
]);
//Total
const total = computed(() => {
  return transactions.value
    .reduce((acc, transaction) => {
      return acc + transaction.amount;
    }, 0)
    .toFixed(2);
});
//income
const income = computed(() => {
  return transactions.value
    .filter((transaction) => transaction.amount > 0)
    .reduce((acc, transaction) => {
      return acc + transaction.amount;
    }, 0)
    .toFixed(2);
});
//expenses
const expenes = computed(() => {
  return transactions.value
    .filter((transaction) => transaction.amount < 0)
    .reduce((acc, transaction) => {
      return acc + transaction.amount;
    }, 0)
    .toFixed(2);
});
</script>
