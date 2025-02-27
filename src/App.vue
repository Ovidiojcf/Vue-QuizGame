<script>
//https://opentdb.com/api.php?amount=25
export default {
  name: 'App',
  data() {
    return {
      question: undefined,
      incorrectAnswers: undefined,
      correctAnswers: undefined,
      chosen_answer: undefined,
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
  created() {
    this.axios.get('https://opentdb.com/api.php?amount=25').then((response) => {
      this.question = response.data.results[0].question;
      this.incorrectAnswers = response.data.results[0].incorrect_answers;
      this.correctAnswers = response.data.results[0].correct_answer;
    })
  },
  methods:{
    submitAnswer(){
      if(!this.chosen_answer){
        alert('Pick one of the options');
      }else{
        if(this.chosen_answer == this.correctAnswers){
          alert('you got ir right');
        }else{
          alert('you failled');
        }
      }
    }
  }
}
</script>

<template>
  <section class="app">
    <template v-if="this.question">
      <div>
        <h1 v-html="this.question"></h1>
      </div>


      <template v-for="(answer, index) in this.answers" :key="index">
        <input type="radio" name="options" :value="answer" v-model="this.chosen_answer">
        <label v-html="answer"></label><br>
      </template>
      <button class="send" type="button" @click="this.submitAnswer()">Send</button>
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
