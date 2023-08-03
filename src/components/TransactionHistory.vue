<template>
  <div class="p-4 bg-gray-400 rounded-lg shadow-lg">
    <h2 class="text-2xl font-bold mb-4">Transaction History</h2>
    <ul class="transaction-list">
      <li v-for="transaction in transactions" :key="transaction.id" class="transaction-item">
        <p class="transaction-date">{{ formatDate(transaction.date) }}</p>
        <div>
          <p class="transaction-type">{{ transaction.type }}:</p>
          <p class="transaction-amount">{{ transaction.amount.toFixed(2) }}</p>
        </div>
        <p class="transaction-category">Category: {{ transaction.category }}</p>
      </li>
    </ul>
  </div>
</template>


<script>
import { ref, computed } from 'vue';

export default {
  setup() {
    const transactions = ref(JSON.parse(localStorage.getItem('transactions')) || []);

    const formatDate = (date) => {
      return new Date(date).toLocaleDateString();
    };

    return {
      transactions,
      formatDate,
    };
  },
};
</script>

<style>
.transaction-list {
  list-style: none;
  padding: 0;
  margin: 0;
}

.transaction-item {
  margin-bottom: 0.5rem;
  padding: 1rem;
  background-color: #f0f0f0;
  border-radius: 0.25rem;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.transaction-date {
  font-size: 0.8rem;
  color: #666;
}

.transaction-type {
  font-size: 0.9rem;
  text-transform: capitalize;
}

.transaction-amount {
  font-size: 1rem;
  font-weight: bold;
}

.transaction-category {
  font-size: 0.8rem;
  color: #888;
}
</style>
  