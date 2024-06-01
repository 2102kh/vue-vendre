<script setup lang="ts">
interface PagingProps{
    currentPage:number;
    totalPages:number;
}
const props = defineProps<PagingProps>()
const emit = defineEmits<{
    (e:'change', newPage:number):void;

}>()
const onPrevPageClick=()=>{
    if(props.currentPage>1){
        emit('change',props.currentPage -1)
    }
}
const onNextPage=()=>{
    if(props.currentPage < props.totalPages){
        emit('change',props.currentPage +1)
    }
}
</script>

<template>
    <div class="pagination">
       <button @click="onPrevPageClick" :disabled="currentPage===1">Föregående</button>
       <span>{{ currentPage }} av {{ totalPages }}</span>
       <button @click="onNextPage" :disabled="currentPage===totalPages">Nästa</button>
    </div>
</template>

<style scoped >

.pagination {
  display: flex;
  justify-content:center;
  align-items: center;
  margin-top: 40px;
  margin-bottom: 30px;
}

button {
  padding: 10px 20px;
  margin: 0 10px;
  border: none;
  /* background-color: #5333ED; */
  background-color: #DD35DD;
  color: white;
  cursor: pointer;
  font-size: 1.2rem;
  border-radius: 5px;
 
}

button:disabled {
  background-color: #ccc;
  cursor: not-allowed;
}

span {
  margin:10px;
  font-size:16px;
}
@media(max-width:500px){
  button{
    padding: 12px 20px;
    font-size: 1rem;
    margin: 5px 10px;
  }
  span{
    font-size: 0.8rem;
  }
}

</style>