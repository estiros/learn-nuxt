<template>
  <b-container>
    <h1 class="text-center mt-5">Login</h1>
    <center>
      <b-form class="col-md-6" @submit.prevent="userLogin">
        <b-form-input
          v-model="user_email"
          placeholder="Email"
          type="email"
          required
          class="mb-2"
        ></b-form-input>
        <b-form-input
          v-model="user_password"
          placeholder="Password"
          type="password"
          required
          class="mb-2"
        ></b-form-input>
        <b-button variant="success" type="submit">Login</b-button>
      </b-form>
    </center>
  </b-container>
</template>

<script>
export default {
  data() {
    return {
      user_email: 'eve.holt@reqres.in',
      user_password: 'cityslicka'
    }
  },
  methods: {
    async userLogin() {
      try {
        const response = await this.$auth.loginWith('local', {
          data: {
            email: this.user_email,
            password: this.user_password
          }
        })
        console.log(response)
      } catch (err) {
        console.log(err)
      }
    }
  }
}
</script>

<style></style>
