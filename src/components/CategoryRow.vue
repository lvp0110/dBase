<template>
        <div 
            @click="getItems(category.Code)" 
            class="list-group-item  list-group-item-action" style="color:white;background:rgb(39, 38, 38);"
        >
        <h6 >{{ category.Code }} | {{ category.Name }} </h6>

        <ItemList v-if="visible" :items="items" :cat="category"/>

        
    </div>
</template>


<script>

import ItemList from './ItemList.vue'


export default {
    props: ['category'],
    components: {
        ItemList
    },
    
    data()
    {
        return {
            items: [],
            visible: false,
            
        }
    },
    methods: {
        async getItems(Id)
        {
            let res = await fetch(`http://158.160.73.203:3005/api/v1/ConstrMaterials/${Id}`);
            let data = await res.json();

            console.log(data)

            // let result = data.filter((el) => el.c_id == Id);

            this.items = data.data;
            this.visible = !this.visible;

      
        }
    }
}
</script>