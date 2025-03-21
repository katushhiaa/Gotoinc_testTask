<template>
  <ul>
    <li v-for="(request, index) in requests" :key="index">
      <div class="request-info">
        <span class="route">{{ request.fromCity }} → {{ request.toCity }}</span>
        <span class="details">({{ request.type }}) | {{ request.date }}</span>
        <p>{{ request.description }}</p>
      </div>
      <div class="buttons">
        <button @click="$emit('edit-request', index)">Редагувати</button>
        <button @click="$emit('delete-request', index)">Видалити</button>
      </div>
    </li>
  </ul>
</template>


<script>
export default {
  name: 'RequestList',
  props: {
    requests: {
      type: Array,
      required: true
    }
  }
}
</script>

<style scoped>
ul {
  list-style: none;
  padding: 0;
}

li {
  background-color: #f9f9f9;
  margin-bottom: 16px;
  padding: 16px 20px;
  border-radius: 12px;
  border: 1px solid #ddd;
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.05);
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.request-info {
  display: flex;
  flex-direction: column;
  gap: 4px;
}

.route {
  font-weight: bold;
  color: #333;
}

.details {
  color: #444;
}

p {
  margin: 8px 0 0 0;
  font-size: 15px;
  color: #555;
}

.buttons {
  display: flex;
  gap: 10px;
  margin-top: 10px;
  justify-content: center;
}

button {
  padding: 6px 12px;
  font-size: 14px;
  border: none;
  border-radius: 6px;
  cursor: pointer;
  transition: 0.2s ease-in-out;
}

button:hover {
  opacity: 0.85;
}

button:nth-child(1) {
  background-color: #ffc107; /* Редагувати */
  color: black;
}

button:nth-child(2) {
  background-color: #dc3545; /* Видалити */
  color: white;
}
</style>

