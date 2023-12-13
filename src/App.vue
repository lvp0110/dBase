<template>
  <div  class="d-grid gap-2 d-md-block" >
    
    <button type="button" class="btn btn-outline-light  " @click="tab = tab == 1 ? 0 : 1" style="align-self: center;" >
      <h1>Конструкции</h1>
    </button>
    <button type="button" class="btn btn-outline-light " style="align-self: center;" 
    @click="tab = tab == 2 ? 0 : 2">
          <h1 style="padding-left: 10px;padding-right: 10px;">Материалы</h1>
    </button>

    <!-- <CategoriesList v-if="unvisible" :categories="Categories" >
      <CategoryRow v-for="category in getSearch" :key="category.id" :category="category" />
       <MaterialInfo v-if="visible"  :material="category"/>
    </CategoriesList> -->

    <CategoriesList v-if="tab == 1" :categories="Categories" @search="searchCategories" >     

      <CategoryRow v-for="category in ResultCategories" :key="category.id" :category="category" @getItems="getItems" >
        <ItemList :items="items" :cat="category"/>
      </CategoryRow>

    </CategoriesList>

    <CategoriesList v-if="tab == 2" :categories="Materials" @search="searchMaterials" >     

      <CategoryRow v-for="category in ResultMaterials" :key="category.id" :category="category" @getItems="() => {}" >
        <MaterialInfo :material="category" />
      </CategoryRow>

    </CategoriesList>
    

  </div>
  
</template>


<script>

/*mport MaterialList from './components/MaterialList.vue'*/
import CategoriesList from './components/CategoriesList.vue';
import CategoryRow from './components/CategoryRow.vue';
import MaterialInfo from './components/MaterialInfo.vue';
import ItemList from './components/ItemList.vue';
import { setTransitionHooks } from 'vue';

export default {
  components: {
    CategoriesList,
    CategoryRow,
    MaterialInfo,
    ItemList
    
  },
  data()
  {
    return {
      Categories: [],
      ResultCategories: [],
      Materials: [],
      ResultMaterials: [],
      unvisibleCat:false,
      unvisibleMat: false,

      tab: 0,

      items: []
    }
  }, 
  /*-----------------------------------*/

    methods:{

        searchCategories(text)
        {
          console.log(text)

          if(text != '')
              this.ResultCategories = this.Categories.filter((el) => el.Name.toLowerCase().includes(text.toLowerCase()));
          else 
              this.ResultCategories = [ ...this.Categories ];

          console.log(this.ResultCategories)
        },

        searchMaterials(text)
        {
          console.log(text)

          if(text != '')
              this.ResultMaterials = this.Materials.filter((el) => el.Name.toLowerCase().includes(text.toLowerCase()));
          else 
              this.ResultMaterials = [ ...this.Materials ];

          console.log(this.ResultMaterials)
        },

        async getItems(Id)
        {
            let res = await fetch(`http://158.160.73.203:3005/api/v1/ConstrMaterials/${Id}`);
            let data = await res.json();

            console.log(data)

            // let result = data.filter((el) => el.c_id == Id);

            this.items = data.data;
        
        },



    async getStartContruction(){
      
  
    let res = await fetch(`http://158.160.73.203:3005/api/v1/ConstrIsolation`);
    let data = await res.json();

    console.log(data.data)

    this.ResultCategories = this.Categories = data.data.filter((el) => el.Visible != false);
    
          
    },
    async getStartMaterial(){
      let res = await fetch(`http://158.160.73.203:3005/api/v1/MaterialsIsolation`);
      let data = await res.json();
      console.log(data.data)


      this.ResultMaterials = this.Materials = data.data;

    }
  
  },
  created()
  {
    this.getStartContruction()
    this.getStartMaterial()
  },
  computed: {
        getSearch()
        {
            if(this.search_constr != '')
                return this.Categories.filter((el) => el.Name.toLowerCase().includes(this.search_constr.toLowerCase()));

            return this.Categories;
        },
    }
 
   

}
</script>