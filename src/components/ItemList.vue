<template>
    
      <div v-if="items.length" class="list-group list-group-flush list-group-item-light" >
         <div class="list-group list-group-flush " > 
            <div class="list-group-item list-group-item-action" style="background:rgb(74, 73, 73);">
               <p class="description" >{{ cat.Description }}</p>
               <img  :src="imagePath" alt=""> 
               <ul>Характеристики:
                  <li>Толщина: {{ cat.Thickness }} мм</li>
                  <li v-if="visiblRw">Rw ≈ {{ cat.SoundIndex }} дБ</li>
                  <li v-if="visiblLnw" >Lnw ≈ {{ cat.ImpactNoseIndex}} дБ</li>
               </ul>
               <br>
               <p class="specification" > {{ cat.Specification }}</p>
            </div>
               <h6 style="margin-top: 8px;">Материалы:</h6>
            <div class="list-group-item list-group-item-action " 
               style="cursor: pointer;background:rgb(74, 73, 73);color: white;" v-for="item in items" :key="item.Code">
                  {{ item.Name }}
            </div>
         </div>
        </div>
   
</template>

<script>

export default {
   data()
    {
           return {
           imageFolder:'./', 
           visible:false, 
           unvisible:true, 
        }
    },
    computed:{
        imagePath(){
            return this.imageFolder + this.cat.Img
        },
         visiblLnw(){
         if(this.cat.ImpactNoseIndex != 0)
           return true;
        },
     
         visiblRw(){
         if(this.cat.SoundIndex != 'неопределен')
           return true;
        }
      
    },
    methods:{
      

    },
    props: ['items','cat']
   
}
</script>

<style scoped>
 ul{
    position: relative;
    display: inline-block;
    color: white;
 }
 img{
    width:50%;
    transition: all .9s;
    border-radius: 2%;
    position: relative;
    cursor: pointer;
    z-index: 11;
 }
 .description{
    text-align: center;
    color:white;
    margin-left:15px;
    justify-content: center;
 }
 .specification{
    color:white;
    margin-top:15px;
    justify-content: center;
    text-align: left;
 }
@media screen and (max-width: 450px){
 img{
    width:100%;
    transition: all .9s;
    border-radius: 2%;
    position: relative;
    cursor: pointer;

 }
}
@media screen and (max-width: 900px){
 img:hover{
    width:94%;
    transition: all .7s;
    position: absolute;background-color: rgb(54, 50, 50);
 }
}
</style>