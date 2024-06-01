<script>
import EmployeeList from './components/EmployeeList.vue';
export default {
 
  components: {
    EmployeeList
  }
}

</script>  
<template>
  <div id="app">
    <h1>Välkommen till Vendre!</h1>
    <h3>Vi är stolta över vårt team av begåvade och dedikerade medarbetrare som bidrar till vår framgång varje dag</h3>
    <EmployeeList /> 
  </div>
  </template>

<style scoped>
#app{
  padding:10% 5%;
  width: 100vw;
  height: 100vh;
  /* background-color: #F7C0FE; */
  background-color:rgb(238,235,252) ; 
  text-align: center;
  display: flex;
  flex-direction: column;
  justify-content: center;
  overflow: hidden;
}
h1{
  color:rgb(83,51,237);
  font-weight: 700;
  margin-bottom: 20px;
}
h3{
  font-weight: 600;
  margin-bottom:20px;
}
@media(max-width:600px){
  #app{
    padding: 6% 2%;
  }
  h1{
    font-size: 1.5rem;
    margin-bottom: 0.3rem;
  }
  h3{
    font-size: 1rem;
    margin-bottom: 0.3rem;
  }

}
</style>
