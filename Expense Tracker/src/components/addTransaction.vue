<template>
  <h3>Add new transaction</h3>
  <form id="form" @submit.prevent="onSubmit">
    <div class="form-control">
      <label for="name">Text</label>
      <input type="text" id="text" placeholder="Enter text..." v-model="name" />
    </div>
    <div class="form-control">
      <label for="amount"
        >Amount <br />
        (negative - expense, positive - income)</label
      >
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
import { ref } from "vue";
import { useToast } from "vue-toastification";

const name = ref("");
const amount = ref("");
const toast = useToast();

//for adding new expense..push from here to catch in app.vue

const emit = defineEmits(["transactionSubmitted"]);

const onSubmit = () => {
  if (!name.value || !amount.value) {
    toast.error("Both are required");
    return;
  }

  const transdata = {
    name: name.value,
    amount: parseFloat(amount.value),
  };

  emit("transactionSubmitted", transdata);
};
name.value = "";
amount.value = "";
</script>