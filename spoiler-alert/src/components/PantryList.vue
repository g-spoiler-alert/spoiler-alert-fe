<template>
  <section class="food-list">
    <food-item
      v-for="(food, index) in foods.items"
      :food="food"
      :get-food="getFood"
      :key="index"/>
  </section>
</template>

<script>
import FoodItem from '@/components/FoodItem'

export default {
  components: {
      FoodItem
  },
  props: ['foods', 'getFood'],
}
</script>

<style>
.food-list{
    display: flex;
    flex-flow: row wrap;
    margin: 1vw;
    justify-content: space-around;
    align-content: space-around;
}
</style>