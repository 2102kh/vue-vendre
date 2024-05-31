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
  <div class="employees-list">
    <div v-for="employee in employees" :key="employee.id" class="employee-card">
      <img :src="employee.avatar"  />
      <p>{{ employee.first_name }} {{ employee.last_name }}</p>
      <a :href="`mailto:${employee.email}`">{{ employee.email }}</a>
    </div>
  </div>
</template>

<style scoped>
.employees-list{
  display: grid;
  flex-wrap: wrap;
  grid-template-columns: repeat(auto-fill, minmax(150px,1fr));
  justify-items: center;
  gap:30px;
} 
.employee-card{
 padding-top: 20px;
 a{
  color:black;
  font-size:700;
 }


}
img{
  border-radius: 50%;
}
</style>
