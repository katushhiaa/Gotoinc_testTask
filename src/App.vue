<script setup>
import {ref} from "vue";
import RequestList  from "./components/RequestList.vue";
import RequestForm from './components/RequestForm.vue'

const requests = ref([]);

const addRequest = (request) =>{
  requests.value.push(request);
};

</script>

<template>
<div>
  <RequestForm @submit-request="addRequest" />
  <RequestList :requests="requests" />
</div>
</template>

<style scoped>

</style>
