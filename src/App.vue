<template lang="html">
  <div>
    <select-category :categories="categories"></select-category>

  </div>
</template>

<script>
import SelectCategory from './components/SelectCategory.vue'
export default {
  name:'app',
  data(){
    return{
      categories: null,
      selectedCategory: null,
      score: 0
    }
  },
  mounted(){
    fetch("https://opentdb.com/api_category.php")
    .then(result => result.json())
    .then(categories => this.categories = categories.trivia_categories)
  },
  components:{
    'select-category': SelectCategory
  }
}
</script>

<style lang="css" scoped>
</style>
