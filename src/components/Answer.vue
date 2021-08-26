<template>
        <!-- SINGLE ANSWER TEMPLATE -->
        <div class="box">
           <input
                type="radio" 
                :id="risposta.indice" 
                name="answers" 
                :value="risposta.indice" 
                v-model="choice"
                @change="$emit('sent', choice)"
                @click="next"
            >
            <label v-if="choice === '' "
                    class="inside"                 
                    :for="risposta.indice">
                    {{risposta.risposta}}
                </label>
                <label v-else class="inside" 
                    :class="{activeTrue : (risposta.risultato === choice), activeFalse : (risposta.risultato != choice)}" 
                    :for="risposta.indice">
                    {{risposta.risposta}}
                </label>
          </div>  
            
       
        
   
</template>

<script>

export default {
    name:"answer",
    props: ["risposta"],
    data(){
        return{
            choice: "",            
        }
    },
    created(){
        this.clear();
    },
    methods:{
        // FUNCTION TO CLEAR CHOICE WHEN ANSWER CHANGE
        clear(){
            this.choice="";
        },
        next(){
            setTimeout(()=>{
                this.clear();
            },3000)
        }
    }
}
</script>
<style scoped lang="scss">


.box{
    flex-basis: calc(100% / 2 - 60px);
    display: flex;
    justify-content: center;
    align-items: center;
    margin: 30px;
    height: 60px;
    background-color:#fff;
    padding: 2px;
    position: relative;
    clip-path: polygon(
         20% 0,
         80% 0%,
         100% 50%,
         80% 100%,
         20% 100%,
         0% 50%);
    word-wrap: break-word;
    color: #fff;
    input{
        position: absolute;
        opacity: 0;
    }
    .inside{
        width: 100%;
        height: 100%;
        display: flex;
        justify-content: center;
        align-items: center;
        background-color:blue;
        padding: 10px 20px;
        clip-path: polygon(
            20% 0,
            80% 0%,
            100% 50%,
            80% 100%,
            20% 100%,
            0% 50%);
        cursor:pointer;
        text-align: center;
        text-transform: capitalize;
    }
    .activeTrue{
        background-color: green !important;
    }
    .activeFalse{
        background-color: red !important;
    }
}

@media screen and (max-width: 400px){
    .box{
        flex-basis: 100%;
    }
}
</style>