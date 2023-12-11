<template>
  <div class="container py-2">
    <button type="button" class="btn btn-outline-light" @click="getStartContruction()">
      <h1>Конструкции</h1>
    </button>
    <button type="button" class="btn btn-outline-light" style="align-self: center; " 
    @click="getStartMaterial()">
      <h1 style="padding-left: 10px;padding-right: 10px;">Материалы</h1>
    </button>

    <CategoriesList v-if="unvisible" :categories="Materials" />
    <CategoriesList v-if="unvisible" :categories="Categories" />
    

  </div>
  
</template>


<script>

/*mport MaterialList from './components/MaterialList.vue'*/
import CategoriesList from './components/CategoriesList.vue'


export default {
  components: {
    CategoriesList,
    
  },
  data()
  {
    return {
      Categories: [],
      Materials: [],
      unvisible:false,
      visible:false,
    }
  }, 
  /*-----------------------------------*/

    methods:{
    async getStartContruction(){
      
  
    let res = await fetch(`http://158.160.73.203:3005/api/v1/ConstrIsolation`);
    let data = await res.json();

    console.log(data.data)

    this.Categories = data.data.filter((el) => el.Visible != false);
    this.unvisible = !this.unvisible;
   
       
    },
    async getStartMaterial(){
      let res = await fetch(`http://158.160.73.203:3005/api/v1/MaterialsIsolation`);
    let data = await res.json();
    this.Categories = data.data;
    this.unvisible = !this.unvisible;

    }
  
  },

}
</script>