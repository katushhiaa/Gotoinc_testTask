<script setup>
import {ref} from "vue";

const emit = defineEmits(['submit-request']);


const fromCity = ref('');
const toCity = ref('');
const type = ref('');
const date = ref('');
const description = ref('');

const submitForm = () =>{
  emit('submit-request', {
    fromCity: fromCity.value,
    toCity: toCity.value,
    type: type.value,
    date: date.value,
    description: description.value,
  });

  fromCity.value = '';
  toCity.value = '';
  type.value = '';
  date.value = '';
  description.value = '';
}

</script>

<template>

  <form @submit.prevent = "submitForm">
    <input v-model="fromCity" placeholder="Введіть місто з якого відправка" required />
    <input v-model="toCity" placeholder="Введіть місто в яке доставка" required />
    <select  v-model="type" required>
      <option value="gadgets">Гаджети</option>
      <option value="drinks">Напої</option>
      <option value="clothes">Одяг</option>
      <option value="medicines">Ліки</option>
      <option value="other">Інше</option>
    </select>

    <input v-model="date" type="date" required />
    <textarea v-model="description" placeholder="Опис" required></textarea>
    <button type="submit">Додати заявку</button>
  </form>


</template>

<style scoped>

</style>