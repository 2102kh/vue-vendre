<script setup lang="ts">
import axios from 'axios';
import { ref, onMounted } from 'vue';
import type { IEmployees } from './models/IEmployees.ts';
import EmployeePagination from './EmployeePagination.vue';



const employees = ref<IEmployees[]>([]);
const currentPage = ref(1);
const totalPages = ref(2);


const getEmployees = async (page: number) => {
  const response = await axios.get<{data:IEmployees[],total_pages:number}>(`https://reqres.in/api/users?page=${page}`);
  console.log( response.data); 
  // employees.value =[...employees.value,...response.data.data];
  employees.value = response.data.data
  console.log(...employees.value); 
  console.log(...response.data.data)
  totalPages.value =response.data.total_pages
};

onMounted(() => {
  getEmployees(currentPage.value);
});
const onPageChanged=(newPage:number)=>{
  currentPage.value= newPage;
  if(newPage<= totalPages.value){
    getEmployees(newPage)
  }
}
</script>

<template>
  <div class="employees-list">
    <div v-for="employee in employees" :key="employee.id" class="employee-card">
      <img :src="employee.avatar"  />
      <p>{{ employee.first_name }} {{ employee.last_name }}</p>
      <a :href="`mailto:${employee.email}`">{{ employee.email }}</a>
    </div> 
  </div>
  <EmployeePagination 
    :current-page="currentPage"
    :total-pages="totalPages"
    @change="onPageChanged"/>
  
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
