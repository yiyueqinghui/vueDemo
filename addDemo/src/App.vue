<template>
  <div id="app">
    <listone></listone>
  </div>
</template>


<script>
import listone from './components/list.vue'
export default {
   name: 'app',
   data(){
   	  return {
   	  	
   	  }
   },
   methods:{
   	 
   	 
   },
   components:{
   	  'listone':listone
   }
   
    
   
  
}
</script>

<style scoped>
*{
	margin: 0;
	padding:0;
	box-sizing: border-box;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  width:100%;
  max-width:900px;
  margin:0 auto;
  color: #2c3e50;
}

</style>
