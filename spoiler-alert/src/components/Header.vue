<template>
  <header>
    <b-navbar
      class="navbar"
      type="light"
      variant="light"
      fixed="top">
      <h1>Spoiler Alert!</h1>
      <div class="login">
        <b-nav-form class="login">
          <b-form-input
            v-model="userName"
            size="sm"
            class="login-text mr-sm-2"
            type="text"
            placeholder="User Name"/>
          <b-button
            type="submit"
            size="sm"
            class="my-2 my-sm-0"
            @click.prevent="getUser(userName)">
            Login</b-button>
        </b-nav-form>
      </div>
    </b-navbar>
  </header>
</template>

<script>

export default {
  props: ['getUser'],
  data() {
    return {
      userName: '',
    }
  }
}
</script>

<style>
.login {
  display: flex;
  flex-direction: row;
  flex-wrap: nowrap;
}

@media (max-width: 500px) {
  .login-text {
    margin-right: 2%
  }
}
</style>
