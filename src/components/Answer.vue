<template lang="html">
<div class="">
<li v-on:click="checkAnswer">{{answer}}</li>

</div>


</template>

<script>
import {eventBus} from'../main.js'
export default {
  name: "Answer",
  props:['answer', 'correct'],
  data(){
    return{
correctCount:0
  }
},
  methods:{
checkAnswer: function(){
  if (this.answer === this.correct){
    alert(`Well Done ${this.answer} is correct`)
    eventBus.$emit('correct-answer')
  }else{
    alert(`Sorry, wrong answer, the correct answer was ${this.correct}`)
  }
  eventBus.$emit('wrong-answer')
}

  }
}
</script>

<style lang="css" scoped>
</style>
