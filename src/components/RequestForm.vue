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

  <form @submit.prevent = "submitForm" class="request-form">
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
.request-form {
  max-width: 500px;
  margin: 40px auto;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 12px;
  display: flex;
  flex-direction: column;
  gap: 15px;
  background-color: #f9f9f9;
}

.request-form input,
.request-form select,
.request-form textarea {
  padding: 10px;
  font-size: 16px;
  border-radius: 8px;
  border: 1px solid #bbb;
  width: 500px;
  box-sizing: border-box;
}

.request-form textarea {
  resize: vertical;
  min-height: 80px;
}

.request-form button {
  padding: 12px;
  background-color: #007bff;
  color: white;
  font-weight: bold;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.request-form button:hover {
  background-color: #0056b3;
}

</style>