<template>
  <main>
      <!-- QUESTIONS -->
      <div class="question">
          <div class="inside">
            {{question}}
          </div>
      </div>
      <!-- ANSWERS -->
      <div>
          <form class="answer-box">
                <Answer
                v-for="(answer, indice) in answers"
                :key="indice"
                :risposta="{risposta:answer, indice:indice, risultato:response}" 
                @sent="getChoice"
                /> 
         </form>
      </div>
  </main>
</template>

<script>
import Answer from '@/components/Answer.vue';
import questions from '@/data/questions.js';
export default {
    name: "Main",
    components:{
        Answer,
    },
    data(){
        return{
            domande: questions,
            question: '',
            answers: {},
            index: 0,
            response:'',
            scelta:'',
            indexAnswers: [],
            result: 0,
            level:0,
            winLoose:'',
        }
    },
    created(){
        this.getQuestions();
    },

    methods:{
        // FUNCTION TO GET QUESTION AND ANSWERS
        getQuestions(){
            // RANDOM NUMBER FOR QUESTIONS
            let number = ''
            do{
                number = Math.floor(Math.random() * 15);
            }while(this.indexAnswers.includes(number))
            

            if(!this.indexAnswers.includes(number)){
                
                this.question = this.domande[this.index].questions[number].question;

                this.answers = this.domande[this.index].questions[number].content;

                this.response = this.domande[this.index].questions[number].correct;
 
                this.indexAnswers.push(number);
                
            }
            
        },
        // FUNCTION TO GET USER CHOICE
        getChoice(choice){
            this.scelta = choice;
            if(this.scelta == this.response){
                this.result++

                // CALCULATE LEVEL
                if(this.indexAnswers.length == 3 && this.level == 0){
                    this.index = 1;
                    this.level = 1;
                    this.indexAnswers = [];
                }else if(this.indexAnswers.length == 3 && this.level == 1){
                    this.index = 2;
                    this.level = 2;
                    this.indexAnswers = [];
                }else if(this.indexAnswers.length == 3 && this.level == 2){
                    this.index = 3;
                    this.level = 3;
                    this.indexAnswers = [];
                }else if(this.indexAnswers.length == 3 && this.level == 3){
                    this.index = 4;
                    this.level = 4;
                    this.indexAnswers = [];
                }else if(this.result == 15 && this.level == 4){
                    this.winLoose = 'HAI VINTO!!  SEI UN MILIONARIO!!'
                    this.results();
                }
            }else{
                this.winLoose = 'Hai perso!!'
                this.results();
            }

            this.next();
        },
        // TIMING FUNCTION TO WAIT 3 SECONDS TO GET NEW QUESTION AND ANSWERS
        next(){
            setTimeout(()=>{
                this.getQuestions();
            },3000)
        },
        // FUNCTION TO GET RESULTS WHEN USER LOOSE OR WIN AND CLEAR ALL VARIABLES
        getResults(){
            alert(`${this.winLoose}
                Il tuo risultato è di ${this.result} punti`);
                this.indexAnswers = [];
                this.result = 0;
                this.level = 0;
                this.winLoose = '';
        },
        // TIMING FUNCTION TO WAIT 2 SECONDS TO GET SCORE
        results(){
            setTimeout(()=>{
                this.getResults();
            },2000)
        },
    }
}
</script>

<style scoped lang="scss">
main{
    flex-grow: 1;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    height: calc(100vh - 280px);
    background-color:#11093A ;
    padding: 50px 0;
    .question{
        height: 50px;
        background-color:#fff;
        padding: 2px;
        clip-path: polygon(
            20% 0,
            80% 0%,
            100% 50%,
            80% 100%,
            20% 100%,
            0% 50%);
        display: flex;
        justify-content: center;
        align-items: center;
        color: #fff;
        text-transform: capitalize;
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
    .answer-box{
        margin-top: 30px;
        width: 100%;
        display: flex;
        justify-content: center;
        flex-wrap: wrap;
    }
}

// MEDIA QUERY FOR RESPONSIVE LAYOUT
@media screen and (max-width: 400px){
    main{
        height:auto;
    }
    .answer-box{
        flex-direction: column;
        width: 400px;
    } 
}
</style>