<script setup>
defineProps({
  requests:Array
});
</script>

<template>
<ul>
  <li v-for="(request, index) in requests" :key="index">
    {{request.from}} -> {{request.toCity}} ({{request.type}}) | {{request.date}}
    <p>{{ request.description}}</p>
  </li>
</ul>
</template>

<style scoped>

</style>