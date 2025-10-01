<template>
  <Header />
  <Balance />
  <IncomeExpence />
  <TransactionList />
  <AddTrasaction />
</template>
<script>
import Header from "./components/Header.vue";
import Balance from "./components/Balance.vue";
import IncomeExpence from "./components/IncomeExpence.vue";
import TransactionList from "./components/TransactionList.vue";
import AddTrasaction from "./components/AddTrasaction.vue";
export default {
  components: {
    Header,
    Balance,
    IncomeExpence,
    TransactionList,
    AddTrasaction,
  },
};
</script>
