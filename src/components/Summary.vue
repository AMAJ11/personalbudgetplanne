<template>
  <v-card class="mb-4">
    <v-card-text>
      <v-row dir="rtl">
        <v-col><strong>دخل:</strong> {{ income }}</v-col>
        <v-col><strong>خرج:</strong> {{ expense }}</v-col>
        <v-col><strong>متبقي:</strong> {{ balance }}</v-col>
      </v-row>
    </v-card-text>
  </v-card>
</template>

<script setup>
import { computed } from 'vue'
const props = defineProps(['transactions'])
const income = computed(() => props.transactions.filter(t => t.type === 'دخل').reduce((sum, t) => sum + t.amount, 0))
const expense = computed(() => props.transactions.filter(t => t.type === 'خرج').reduce((sum, t) => sum + t.amount, 0))
const balance = computed(() => income.value - expense.value)
</script>

