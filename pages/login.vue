.<template>
  <b-container>
    <h1 class="text-center mt-5">Login</h1>
    <center>
      <b-form class="col-md-6" @submit="submitLogin">
        <b-form-input
          v-model="email"
          placeholder="Email"
          type="email"
          required
          class="mb-2"
        ></b-form-input>
        <b-form-input
          v-model="password"
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
export default {}
</script>

<style></style>
