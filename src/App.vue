<template>
  <div id="app">
    <Header />
    <div class="content">
      <Calender />
    </div>             
  </div>
</template>

<script>
  import Header from './components/Header.vue'
  import Calender from './components/Calender.vue'
export default {
  name: 'App',
  components: {
    Header,
    Calender
  }
}
</script>
<style scoped>
   .table th,td{
      text-align: center;
   }
   .table td{
      padding:20px; 
      font-size: 20px;
   }
   .table td:hover{
      background-color: #eee;
   }
   .table-bordered td,th {
      border: 4px solid #dee2e6d1;
  }
</style>

