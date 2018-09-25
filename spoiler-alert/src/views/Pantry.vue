<template>
  <div id="pantry">
    <div class="welcome">
      <h3 class="page-title">Welcome to your pantry {{ userName }}!</h3>
    </div>
    <Form
      :get-food="getFood"
      :user-id="userId"/>
    <b-button
      class="main-button"
      type="button"
      variant="primary"
      @click.prevent="getFood()">Your pantry
    </b-button>
    <article v-if="showPantry">
      <pantry-list
        :foods="foods"
        :get-food="getFood"/>
    </article>
  </div>
</template>

<script>
import Form from '@/components/Form'
import PantryList from '@/components/PantryList'

export default {
  components: {
    Form,
    PantryList
  },
  props: {
     userId: {
      type: Number,
      required: true
    },
    userName: {
      type: String,
      default: String,
      required: true
    }
  },
  data() {
    return {
    showPantry: true,
    foods: []
    }
  },
  methods: {
    getFood() {
      const apiUrl = `https://g-spoiler-alert.herokuapp.com/api/v1/pantry/${this.userId}`
      fetch(apiUrl)
      .then(Response => Response.json())
      .then(Response => {
        this.foods = Response
      })
    }
  }
}

</script>

<style>
#pantry {
  background-image: url(https://cdn-images-1.medium.com/max/2000/1*wfoo4AtOkOWSUq-7rIT53Q.jpeg);
  min-height: 87vh;
  color: white;
  padding-top: 2%;
  background-attachment: fixed;
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
}

.welcome {
  background-color: rgba(0, 0, 0, 0.5);
  margin-top: -1.4%;
  padding-top: .5em;
  padding-bottom: .5em;
}

@media (max-width: 500px) {
  .welcome {
    margin-top: 14.5%;
  }
}
</style>
