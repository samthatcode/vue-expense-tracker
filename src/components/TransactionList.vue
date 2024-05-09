<template>
  <h3>History</h3>
  <ul id="list" class="list">
    <!--iterates over the transactions array received as a prop & displays a list of transactions fetched from the parent component -->
    <li
      v-for="transaction in transactions"
      :key="transaction.id"
      :class="transaction.amount < 0 ? 'minus' : 'plus'"
    >
      {{ transaction.text }} <span>&#x20A6;{{ transaction.amount }}</span>
      <button class="delete-btn" @click="deleteTransaction(transaction.id)">
        X
      </button>
    </li>
  </ul>
</template>

<script setup>
import { defineProps } from 'vue';

const props = defineProps({
  transactions: {
    type: Array,
    required: true,
  },
});

// the transactionDeleted event is emitted with the transaction ID to the parent component
const emit = defineEmits(['transactionDeleted']);

const deleteTransaction = (id) => {
  emit('transactionDeleted', id);
};
</script>
