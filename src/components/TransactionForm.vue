<template>
  <div>
    <input v-model="amount" type="number" class="border p-2  rounded" placeholder="Amount" />
    <select v-model="type" class="border p-2 m-2 rounded">
      <option value="Income">Income</option>
      <option value="Expense">Expense</option>
    </select>
    <select v-model="category" class="border p-2 m-2 rounded" v-if="type === 'Expense'">
      <option value="Food">Food</option>
      <option value="Transport">Transport</option>
      <option value="Housing">Housing</option>
      <!-- Add more expense categories as needed -->
    </select>
    <input v-model="date" type="date" class="border p-2 rounded" />
    <button @click="addTransaction" class="bg-blue-500 hover:bg-blue-600 text-white px-4 py-2 rounded">
    Add Transaction
    </button>
  </div>
</template>

<script>
import { ref } from 'vue';

export default {
  emits: ['transactionAdded'],
  setup(_, { emit }) {
    const amount = ref('');
    const type = ref('Income');
    const category = ref('Salary');
    const date = ref('');

    const addTransaction = () => {
      if (amount.value !== '' && !isNaN(amount.value)) {
        const transaction = {
          id: Date.now(),
          type: type.value,
          amount: parseFloat(amount.value),
          category: category.value,
          date: date.value,
        };
        emit('transactionAdded', transaction);
        amount.value = '';
        date.value = '';
      }
    };					

    return {
      amount,
      type,
      category,
      date,
      addTransaction,
    };
  },
};
</script>

<style>

</style>
