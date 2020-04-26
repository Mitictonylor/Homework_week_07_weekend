<template lang="html">
  <div class="collector">
    <select-category class="select" :categories="categories"></select-category>
    <questions class="question" v-if="selectedCategoryId" :selectedCategoryId="selectedCategoryId" :token="token"></questions>

  </div>
</template>

<script>
import SelectCategory from './components/SelectCategory.vue'
import Questions from './components/Questions.vue'
import {eventBus} from'./main.js'

export default {
  name:'app',
  data(){
    return{
      categories: null,
      selectedCategoryId: null,
      score: 0,
      token: '',
    }
  },
  mounted(){
    fetch("https://opentdb.com/api_category.php")
    .then(result => result.json())
    .then(categories => this.categories = categories.trivia_categories)


    eventBus.$on('selected-category-id', (selectedCatId) =>{
      this.selectedCategoryId = selectedCatId})
      // fetch token to avoid same questions
    fetch("https://opentdb.com/api_token.php?command=request")
    .then(result => result.json()).then(data => this.token = data.token)
},
  components:{
    'select-category': SelectCategory,
    'questions': Questions
  }
}
</script>

<style lang="css" scoped>

  .select{}
    .question{}
</style>
