<template>
  <div class="p-4 bg-gray-400 rounded-lg shadow-lg">
    <h2 class="text-2xl font-bold mb-4">Dashboard</h2>
    <div class="grid gap-4">
      <div class="card bg-green-400">
        <h3 class="total-label">Total Income</h3>
        <p class="total-amount text-green-800">{{ totalIncome.toFixed(2) }}</p>
      </div>
      <div class="card bg-red-400">
        <h3 class="total-label">Total Expenses</h3>
        <p class="total-amount text-red-800">{{ totalExpenses.toFixed(2) }}</p>
      </div>
      <div class="card bg-blue-400">
        <h3 class="total-label">Available Savings</h3>
        <p class="total-amount text-blue-800 ">{{ availableSavings.toFixed(2) }}</p>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, computed, watchEffect } from 'vue';

export default {
  setup() {
    const transactions = ref(JSON.parse(localStorage.getItem('transactions')) || []);

    const totalIncome = computed(() => {
      return transactions.value
        .filter((transaction) => transaction.type === 'Income')
        .reduce((sum, transaction) => sum + transaction.amount, 0);
    });

    const totalExpenses = computed(() => {
      return transactions.value
        .filter((transaction) => transaction.type === 'Expense')
        .reduce((sum, transaction) => sum + transaction.amount, 0);
    });

    const availableSavings = computed(() => {
      return totalIncome.value - totalExpenses.value;
    });

   
    watchEffect(() => {
      localStorage.setItem('transactions', JSON.stringify(transactions.value));
    });

    return {
      transactions,
      totalIncome,
      totalExpenses,
      availableSavings,
    };
  },
};

</script>

<style>

.grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 1rem;
}

.card {
  background-color: #f5f5f5;
  padding: 1rem;
  border-radius: 0.5rem;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

.total-label {
  font-size: 0.8rem;
}

.total-amount {
  font-size: 1.5rem;
  font-weight: bold;
}

.available-savings {
  margin-top: 1.5rem;
  font-size: 1.2rem;
}

.transaction-history {
  margin-top: 2rem;
  background-color: #f5f5f5;
  padding: 1rem;
  border-radius: 0.5rem;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

.transaction-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0.5rem 0;
  border-bottom: 1px solid #ccc;
}

.transaction-date {
  font-size: 0.8rem;
}

.transaction-amount {
  font-size: 1rem;
  font-weight: bold;
}

.transaction-type {
  text-transform: capitalize;
}

.transaction-category {
  font-size: 0.8rem;
  color: #666;
}

</style>