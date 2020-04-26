<template lang="">
<div >
<button type="button" v-on:click="randomQuestion"name="button">Generate</button>
<p>{{question.question}}</p>
<ul

<answer v-for="answer in shuffle(answers)" :correct="correct" :answer="answer"></answer>


</ul>
<p>Correct answers : {{counter}}</p>
</div>
</template>

<script>
import {eventBus} from'../main.js'
import Answer from './Answer.vue'
export default {
  name:'questions',
  props:['selectedCategoryId','token'],
  data(){
    return{
    questions:null,
    question:'',
    answers: '',
    counter:0,
    correct: "",
    url: `https://opentdb.com/api.php?amount=50&category=${this.selectedCategoryId}&token=${this.token}&type=multiple`
  }
},
computed:{
  //refresh url
},
methods:{
  shuffle: function(arra1) {
    let ctr = arra1.length
    let temp
    let index

// While there are elements in the array
    while (ctr > 0) {
// Pick a random index
        index = Math.floor(Math.random() * ctr);
// Decrease ctr by 1
        ctr--;
// And swap the last element with it
        temp = arra1[ctr];
        arra1[ctr] = arra1[index];
        arra1[index] = temp;
    }
    return arra1;
},
    randomQuestion: function(){
    const query = this.questions[Math.floor(Math.random() * this.questions.length)]
    const incorrect = query.incorrect_answers.map(answer => answer)
    incorrect.push(query.correct_answer)
    this.answers= incorrect
    this.question= query
    this.correct = query.correct_answer

  }
},
mounted(){
  fetch(this.url).then(response=> response.json()).then(data => this.questions = data.results)

  eventBus.$on('correct-answer', (pass) =>{
    this.counter ++;
  this.randomQuestion()})

  eventBus.$on('wrong-answer', () => {this.randomQuestion()})
},
components: {
  'answer':Answer
}
}
</script>

<style lang="css" scoped>
</style>
