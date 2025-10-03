<template>
  <Header />
  <Balance :total="total" />
  <IncomeExpence :income="+income" :expenes="+expenes" />
  <TransactionList
    :transactions="transactions"
    @transactionDeleted="handleTransactionDelete"
  />
  <AddTrasaction @trasactionSubmited="handleTransactionSubmit" />
</template>
<script setup>
import { ref, computed, onMounted } from "vue";
import Header from "./components/Header.vue";
import Balance from "./components/Balance.vue";
import IncomeExpence from "./components/IncomeExpence.vue";
import TransactionList from "./components/TransactionList.vue";
import AddTrasaction from "./components/AddTrasaction.vue";
import { useToast } from "vue-toastification";

const toast = useToast();

const transactions = ref([]);

onMounted(() => {
  const savedTransactions = JSON.parse(localStorage.getItem("transactions"));

  if (savedTransactions) {
    transactions.value = savedTransactions;
  }
});
//Total
const total = computed(() => {
  return transactions.value.reduce((acc, transaction) => {
    return acc + transaction.amount;
  }, 0);
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

const handleTransactionSubmit = (trasactiondata) => {
  transactions.value.push({
    id: transactionID(),
    text: trasactiondata.text,
    amount: trasactiondata.amount,
  });

  saveTransactionsToLocalStorage();
  toast.success("Trasaction Add");
};

const transactionID = () => {
  return Math.floor(Math.random() * 100);
};

const handleTransactionDelete = (id) => {
  transactions.value = transactions.value.filter(
    (transaction) => transaction.id !== id
  );

  saveTransactionsToLocalStorage();
  toast.success("Transaction deleted");
};

const saveTransactionsToLocalStorage = () => {
  localStorage.setItem("transactions", JSON.stringify(transactions.value));
};
</script>
