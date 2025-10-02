<template>
  <h3>History</h3>

  <ul id="list" class="list">
    <li
      v-for="transaction in transactions"
      :key="transaction.id"
      :class="transaction.amount < 0 ? 'minus' : 'plus'"
    >
      {{ transaction.text }} <span>{{ transaction.amount }}</span>
      <button class="delete-btn">x</button>
    </li>
  </ul>
</template>
<script setup>
const transactions = [
  { id: 1, text: "flower", amount: -19.99 },
  { id: 2, text: "salary", amount: 299.97 },
  { id: 3, text: "Book", amount: -34 },
  { id: 4, text: "camera", amount: 140.97 },
];
</script>
