<template>
        <div 
            @click="toggleInfo" 
            class="list-group-item  list-group-item-action" style="color:white;background:rgb(39, 38, 38);"
        >
        <h6 >{{ filterVariable(category.Code) }} | {{ category.Name }} </h6>

        <div v-if="visible">
            <slot></slot>
        </div>
    </div>
</template>

<script>

import ItemList from './ItemList.vue'
import MaterialInfo from './MaterialInfo.vue'

export default {
    props: ['category'],
    components: {
        ItemList,
        MaterialInfo
    },
    
    data()
    {
        return {
            items: [],
            visible: false,
            
        }
    },
    methods: {
        filterVariable(variable) {
            // Проверяем, является ли первый символ цифрой
            if (/^\d/.test(variable)||variable.startsWith('AG')) {
              return variable;
            } else {
              return "---";
            }
          },
       toggleInfo()
       {
            this.visible = !this.visible;
            this.$emit('getItems', this.$props.category.Code)
       }
    }
}
</script>