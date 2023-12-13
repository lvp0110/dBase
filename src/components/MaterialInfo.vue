<template>
    
    <div class="list-group list-group-flush list-group-item-light" >
        <div class="list-group list-group-flush " > 
            <div class="list-group-item list-group-item-action" style="background:rgb(50, 50, 50);">
                <p class="description" >{{ material.Description }}</p>
                <img  :src="imagePath" alt="" > 
                    <ul >Характеристики:
                        <li v-if="material.Length !=0">Длина = {{ material.Length }} мм</li>
                        <li v-if="material.Width !=0"> Ширина = {{ material.Width}} мм</li>
                        <li v-if="material.Height !=0">Толщина = {{ material.Height}} мм</li>
                    </ul>
                <br>
                <p class="specification" > {{ material.Specification }}</p>
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
                return this.imageFolder + this.material.Img
            },
           
        },
   
        props: ['material']
 
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