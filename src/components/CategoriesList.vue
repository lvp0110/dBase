<template>
    <div class="row justify-content-center">
        <div   class="col-15" style="margin-top:10px;">
            <div v-if="categories.length" class="list-group">
                <input  type="text" class="form-control" placeholder="Поиск.." @input="$emit('search', $event.target.value)" style="margin-bottom:10px;"> 


                <slot></slot>            
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
    props: ['categories']
    
}
</script>