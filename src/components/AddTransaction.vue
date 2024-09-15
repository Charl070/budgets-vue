<template>
    <h3>Add new transaction</h3>
      <form id="form" @submit.prevent="onSubmit">
        <div class="form-control">
          <label for="text">Text</label>
          <input type="text" id="text" v-model="text" placeholder="Enter text..." />
        </div>
        <div class="form-control">
          <label for="amount"
            >Amount <br />
            (negative - expense, positive - income)</label
          >
          <input type="text" id="amount" v-model="amount" placeholder="Enter amount..." />
        </div>
        <button class="btn">Add transaction</button>
      </form>
</template>


<script setup lang="ts">

import { ref } from 'vue'
import {useToast} from 'vue-toastification'

const toast = useToast()
const emit = defineEmits(['transactionSubmited'])
const text = ref('');
const amount = ref('');
 const onSubmit = () => {
     if(!text.value || !amount.value) {
         toast.error("Both fields are required");
         return;
     }
     const transactionData={
        text: text.value,
        amount: +amount.value
     }

     emit('transactionSubmited', transactionData)

     text.value = '';
     amount.value = '';
 }
</script>