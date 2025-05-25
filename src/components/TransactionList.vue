<template>
  <v-card class="mb-4">
    <v-list>
      <v-list-item v-for="t in transactions" :key="t.id">
        <v-list-item-content>
          <v-list-item-title>
            {{ t.amount }} - {{ t.category }} ({{ t.type }})
          </v-list-item-title>
          <v-list-item-subtitle>
            {{ t.date }} - {{ t.notes }}
          </v-list-item-subtitle>
        </v-list-item-content>
        <v-btn icon @click="$emit('delete', t.id)"><v-icon>mdi-delete</v-icon></v-btn>
      </v-list-item>
    </v-list>
  </v-card>
</template>

<script setup>
const props = defineProps(['transactions'])
const emit = defineEmits(['delete'])
</script>

