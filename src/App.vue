<template>
  <v-app>
    <v-container class="pa-4 pt-16" max-width="800">
      <Summary :transactions="transactions" />
      <TransactionForm @add-transaction="addTransaction" />
      <TransactionList :transactions="transactions" @delete="deleteTransaction" />
     <div style="width: 70%; margin: auto;"><ExpenseChart :transactions="transactions" /></div>
    </v-container>
  </v-app>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import Summary from './components/Summary.vue'
import TransactionForm from './components/TransactionForm.vue'
import TransactionList from './components/TransactionList.vue'
import ExpenseChart from './components/ExpenseChart.vue'

const transactions = ref([])

onMounted(() => {
  const data = localStorage.getItem('transactions')
  if (data) transactions.value = JSON.parse(data)
})

const save = () => {
  localStorage.setItem('transactions', JSON.stringify(transactions.value))
}

const addTransaction = (t) => {
  transactions.value.push({ ...t, id: Date.now() })
  save()
}

const deleteTransaction = (id) => {
  transactions.value = transactions.value.filter(t => t.id !== id)
  save()
}
</script>
