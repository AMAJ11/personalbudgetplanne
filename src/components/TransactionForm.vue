<template>
  <v-form @submit.prevent="submit">
    <v-row dense>
      <v-col cols="4">
        <v-text-field v-model.number="amount" label="القيمة" type="number" required />
      </v-col>
      <v-col cols="4">
        <v-select :items="['دخل', 'خرج']" v-model="type" label="نوع" required />
      </v-col>
      <v-col cols="4">
        <v-select :items="categories" v-model="category" label="الصنف" required />
      </v-col>
    </v-row>
    <v-text-field v-model="Other" v-if="category=='غير ذلك'" label="غير ذلك" />
    <v-text-field v-model="notes" label="ملاحظات" />
    <div style="width: 100%;display: flex;align-items: center;justify-content: center;">
    <v-btn style="width: 200px;" type="submit" color="primary" class="mb-5">إضافة</v-btn>
</div>
  </v-form>
</template>

<script setup>
import { ref } from 'vue'
const emit = defineEmits(['add-transaction'])
const amount = ref(null)
const type = ref('خرج')
const category = ref('طعام')
const notes = ref('')
const Other = ref('')
const categories = ['طعام', 'نقل', 'تسوق', 'راتب', 'غير ذلك']

const submit = () => {
  if (!amount.value || !type.value || !category.value) return
  if(category.value=="Other"){
    emit('add-transaction', {
    amount: amount.value,
    type: type.value,
    category: Other.value,
    notes: notes.value,
    date: new Date().toISOString().split('T')[0],
})
  }
  else{
  emit('add-transaction', {
    amount: amount.value,
    type: type.value,
    category: category.value,
    notes: notes.value,
    date: new Date().toISOString().split('T')[0],
  })
}
  amount.value = null
  notes.value = ''
  Other.value=''
}
</script>
