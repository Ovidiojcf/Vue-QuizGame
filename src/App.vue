<script>
//https://opentdb.com/api.php?amount=25
import ScoreBoard from './components/ScoreBoard.vue';

export default {
  name: 'App',
  components:{
    ScoreBoard
  },
  data() {
    return {
      question: undefined,
      incorrectAnswers: undefined,
      correctAnswers: undefined,
      chosenAnswer: undefined,
      answerSubmitted: false,
      winCount: 0,
      loseCount: 0
    }
  },
  computed: {
    answers() {
      var answers = [...this.incorrectAnswers];
      answers.splice(Math.round(Math.random() * answers.length), 0, this.correctAnswers); //metodo para bagunçar/alternar as respostas
      return answers;
    }
  }
  ,
  methods:{
    submitAnswer(){
      if(!this.chosenAnswer){
        alert('Pick one of the options');
      }else{
        this.answerSubmitted = true;
        if(this.chosenAnswer == this.correctAnswers){
          this.winCount++;
        }else{
          this.loseCount++;
        }
      }
    },

    getNewQuestion(){
      this.answerSubmitted = false;
      this.chosenAnswer = undefined;
      this.question = undefined;
      this.axios.get('https://opentdb.com/api.php?amount=25').then((response) => {
      this.question = response.data.results[0].question;
      this.incorrectAnswers = response.data.results[0].incorrect_answers;
      this.correctAnswers = response.data.results[0].correct_answer;
    })
    }
  },
  created() {
    this,this.getNewQuestion();
  }
}
</script>

<template>
  <section class="app">
    <ScoreBoard :winCount="this.winCount" :loseCount="this.loseCount" />
    <template v-if="this.question">
      <div>
        <h1 v-html="this.question"></h1>
      </div>


      <template v-for="(answer, index) in this.answers" :key="index">
        <input :disable="this.answerSubmitted" type="radio" name="options" :value="answer" v-model="this.chosenAnswer">
        <label v-html="answer"></label><br>
      </template>

      <button v-if="!this.answerSubmitted" class="send" type="button" @click="this.submitAnswer()">Send</button>

      <section v-if="this.answerSubmitted">
        <h4 v-if="this.chosenAnswer == this.correctAnswers">Congratulations, the answer {{ this.correctAnswers }} is correct</h4>
        <h4 v-else>I'm sorry, you picked the wrong answer.The correct answer is {{ this.correctAnswers }}</h4>
        <button  @click="this.getNewQuestion()" class="send" type="button">Next Question</button>
      </section>
    </template>



  </section>
</template>

<style scoped>
.app {
  font-family: Avenir, Arial, Helvetica, sans-serif;
  font-size: 40px;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothinig: graysacel;
  text-align: center;
  color: #2c3e50;
  margin: 60px;
  max-width: 960px;
}

.app button.send {
  margin-top: 12px;
  height: 40px;
  min-width: 120px;
  padding: 0 16px;
  color: #fff;
  background-color: #1867c0;
  border: 1 px solid #1867c0;
  cursor: pointer;
}
</style>
