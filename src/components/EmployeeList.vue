<script setup lang="ts">
import axios from 'axios';
import { ref, onMounted } from 'vue';
import { IEmployees } from './models/IEmployees.ts';

const employees = ref<IEmployees[]>([]);

const getEmployees = async () => {
  const response = await axios.get<IEmployees[]>('https://reqres.in/api/users');
  console.log( response.data); 
  employees.value = response.data.data
  console.log(employees.value); 
};

onMounted(() => {
  getEmployees();
});
</script>

<template>
  <div>
    <div v-for="employee in employees" :key="employee.id">
      <p>{{ employee.first_name }} {{ employee.last_name }}</p>
      <img :src="employee.avatar"  />
    </div>
  </div>
</template>

<style scoped>

</style>
