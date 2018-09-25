<template>
  <div id="app">
    <Header
      :getUser="getUser"/>
    <router-view
      :user-name="userInput"
      :user-id="userId"/>
    <Footer />
  </div>
</template>

<script>
import Header from '@/components/Header'
import Footer from '@/components/Footer'

export default {
  name: 'App',
  components: {
    Header,
    Footer
  },
  data() {
    return {
      userInput: '',
      userId: null
    }
  },
  methods: {
    getUser(username) {
      this.userInput = username;
      this.findUserId(username);
      ;
    },
    findUserId(username) {
      const apiUrl = `https://g-spoiler-alert.herokuapp.com/api/v1/users/${username}`;
      fetch(apiUrl)
        .then(Response => Response.json())
        .then(Response => {
          console.log(Response.user[0])
          this.userId =  Response.user[0].id
        })
        .then(this.$router.push('pantry'))

    },
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  margin-top: 60px;
  display: flex;
  flex-direction: column;
  min-height:100%;
  position:relative;
}
</style>
