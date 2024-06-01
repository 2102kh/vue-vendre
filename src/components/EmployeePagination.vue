<script setup lang="ts">
import{defineProps,defineEmits} from 'vue';
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
    <div class="buttons">
       <button @click="onPrevPageClick" :disabled="currentPage===1">Föregående</button>
       <span>{{ currentPage }}av {{ totalPages }}</span>
       <button @click="onNextPage" :disabled="currentPage===totalPages">Nästa</button>
    </div>
</template>

<style scoped >

.pagination {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 20px;
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
  margin-top: 2.8rem;
}

button:disabled {
  background-color: #ccc;
  cursor: not-allowed;
}

span {
  margin: 0 10px;
  font-size: 16px;
}
/* .buttons{
  background-color:rgb(238,235,252) ; 
  padding-bottom: 20px;
  width: 100vw;
} */
</style>