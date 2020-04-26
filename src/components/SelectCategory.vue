<template lang="html">
  <div>
  <label for="categorys">SELECT CATEGORY</label>
  <select  id="categorys" v-on:change="handleCategory" v-model="selectedCatId">
    <option disabled value="">Select a Category</option>
    <option v-for="category in categories" :value="category.id" >{{category.name}}</option>
  </select>
  </div>
</template>

<script>
import {eventBus} from'../main.js'
export default {
  name:'SelectCategory',
  data(){
    return{
      selectedCatId:null

  }},
  props:["categories"],
  methods:{
    handleCategory: function(){
        eventBus.$emit('selected-category-id', this.selectedCatId)
      }
    }
  }

</script>

<style lang="css" scoped>
</style>
