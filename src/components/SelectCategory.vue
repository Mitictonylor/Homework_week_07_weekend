<template lang="html">
  <div>
  <label for="categorys">SELECT CATEGORY</label>
  <select  id="categorys" v-on:change="handleCategory" v-model="selectedCat">
    <option disabled value="">Select a Category</option>
    <option v-for="category in categories" :value="category" >{{category.name}}</option>
  </select>
  </div>
</template>

<script>
import {eventBus} from'../main.js'
export default {
  name:'SelectCategory',
  data(){
    return{
      selectedCat:null

  }},
  props:["categories"],
  methods:{
    handleCategory: function(){
        eventBus.$emit('input', this.selectedCat)
      }
    }
  }

</script>

<style lang="css" scoped>
</style>
