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
      <img :src="employee.avatar"  class="img-avatar"/>
      <p>{{ employee.first_name }} {{ employee.last_name }}</p>
      <a :href="`mailto:${employee.email}`">{{ employee.email }}</a>
    </div> 
  </div>
  <div>
  <EmployeePagination 
    :current-page="currentPage"
    :total-pages="totalPages"
    @change="onPageChanged"/>
  </div>
</template>

<style scoped>
.employees-list{
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(150px,1fr));
  justify-items: center;
  gap:30px;
  width: 100%;
  height: auto;
  margin-top: 40px;
} 
.employee-card a{
 padding-top: 20px;
 text-align: center;
 color:black;
}
 
.img-avatar{
  width: 120px;
  height: 120px;
  object-fit: cover;
  border-radius: 50%;
  
}
@media(max-width:550px){
  .employees-list{
    grid-template-columns: 1/2;
    gap:20px;
    padding: 3%;
    margin-top: 10px;
  }
  .img-avatar{
    width:90px;
    height:90px;
  }
}
</style>
