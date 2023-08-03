<template>
  <div class="bg-gray-100 min-h-screen p-8">
    <div class="container mx-auto">
      <Dashboard />
      <div class="grid grid-cols-1 md:grid-cols-2 gap-8 mt-8">
        <TransactionForm @transactionAdded="addTransaction" />
        <TransactionHistory />
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue';
import Dashboard from './components/Dashboard.vue';
import TransactionForm from './components/TransactionForm.vue';
import TransactionHistory from './components/TransactionHistory.vue';


export default {
  components: {
    Dashboard,
    TransactionForm,
    TransactionHistory,
  },
  setup() {
    const transactions = ref(JSON.parse(localStorage.getItem('transactions')) || []);

    const addTransaction = (transaction) => {
      transactions.value.push(transaction);
      localStorage.setItem('transactions', JSON.stringify(transactions.value));
    };

    return {
      addTransaction,
    };
  },
};
</script>

<style>

</style>