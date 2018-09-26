<template>
  <div>
    <b-card
      :title="food.name"
      img-top
      tag="article"
      style="max-width: 20rem;"
      class="mb-2">
      <img
        :src="foodImg"
        alt="image of food type">
      <p class="card-text">
        {{ food.expDate | moment("dddd, MMMM Do") }}
      </p>
      <b-button
        variant="outline-success"
        @click="showDates = !showDates">Update
      </b-button>
      <b-button
        variant="danger"
        @click="deleteFood(food)">Delete
      </b-button>
      <div
        v-if="showDates"
        class="update" >
        <b-form-group
          id="date"
          label="New Expiration Date:"
          label-for="date">
          <b-form-input
            id="date"
            v-model="newExpDate"
            type="date"
            required-placeholder="Expiration date"/>
        </b-form-group>
        <b-button
          variant="success"
          @click="updateFood(food)" >Submit</b-button>
      </div>
    </b-card>
  </div>
</template>

<script>
  export default {
    props: ['food', 'getFood'],
    data() {
      return {
        newExpDate: 'date',
        showDates: false,
        foodType: this.food.type,
        imageSource: '',
        foodImg: require(`../assets/${this.food.type}.jpg`),
      }
    },
    methods: {
      deleteFood(deletedFood) {
        const apiUrl = `https://pacific-caverns-33400.herokuapp.com/api/v1/pantry/delete/${deletedFood.id}`
        fetch(apiUrl, {
            method: "DELETE",
            body: JSON.stringify(deletedFood),
            headers: new Headers({
              "content-type": "application/json"
            })
          })
          .then(data => {
            this.getFood();
          })
          .then(console.log('deleted'))
      },
      updateFood(updateFood) {
        const updateURL = `https://pacific-caverns-33400.herokuapp.com/api/v1/pantry/item/${updateFood.id}`
        fetch(updateURL, {
            method: "PUT",
            headers: new Headers({
              "content-type": "application/json"
            }),
            body: JSON.stringify({
              "expDate": this.newExpDate
            })
          })
          .then(response => response.json())
          .then(data => {
            this.getFood()
            this.showDates = false
          })
      }
    }
  }

</script>

<style scoped>
  article {
    box-shadow: 4px 8px 8px rgba(0, 0, 0, .5);
  }

  div {
    color: black;
    padding-bottom: 2em;
  }

  img {
    height: 120px;
    width: 240px;
  }
</style>
