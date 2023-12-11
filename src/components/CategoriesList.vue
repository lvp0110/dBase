<template>
    <div class="row justify-content-center">
        <div   class="col-15" style="margin-top:10px;">
            <div v-if="categories.length" class="list-group">
                <input  type="text" class="form-control" placeholder="Поиск.." v-model="search_constr" style="margin-bottom:10px;"> 

                <CategoryRow v-for="category in getSearch" :key="category.id" :category="category" />
               
            </div>

            <h2 v-else class="text-muted">Data not found</h2>
        </div>
    </div>
</template> 

<script>

import CategoryRow from './CategoryRow.vue'

export default {
    components: {
        CategoryRow
    },
    props: ['categories'],
    
    data()
    {
    return {
      category: [],
      
      search_constr: '',
        }
    }, 
      computed: {
        getSearch()
        {
            if(this.search_constr != '')
                return this.categories.filter((el) => el.Name.toLowerCase().includes(this.search_constr.toLowerCase()));

            return this.categories;
        },
        
  },
   
    
}
</script>