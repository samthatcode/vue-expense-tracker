<template>
  <h3>Add new transaction</h3>

   <!-- form to add new transactions -->
  <form id="form" @submit.prevent="onSubmit">
    <div class="form-control">
      <label for="text">Expense</label>
      <input type="text" id="text" placeholder="Enter expense..." v-model="text" />
    </div>
    <div class="form-control">
      <label for="amount">Amount <br />
        (negative - expense, positive - income)
      </label>
      <input
        type="text"
        id="amount"
        placeholder="Enter amount..."
        v-model="amount"
      />
    </div>
    <button class="btn">Add transaction</button>
  </form>
</template>

<script setup>
import { useToast } from 'vue-toastification';
import { ref } from 'vue';

const text = ref('');
const amount = ref('');

// Get toast interface
const toast = useToast();

// emits transaction event to parent component if form is valid 
const emit = defineEmits(['transactionSubmitted']);

const onSubmit = () => {
  if (!text.value || !amount.value) {
    // Display a toast error message if either field is empty
    toast.error('Both fields must be filled.', {
      timeout: 1000
    });
    return;
  }

  const transactionData = {
    text: text.value,
    amount: parseFloat(amount.value),
  };

  // emits a transactionSubmitted event with the transaction data
  emit('transactionSubmitted', transactionData);

  // Clear form fields for next transaction entry
  text.value = '';
  amount.value = '';
};
</script>
