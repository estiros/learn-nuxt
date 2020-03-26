<template>
  <div>
    <b-navbar toggleable="lg" type="dark" variant="info">
      <b-navbar-brand href="/">Home</b-navbar-brand>

      <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

      <b-collapse id="nav-collapse" is-nav>
        <b-navbar-nav>
          <b-nav-item href="/album">Album</b-nav-item>
        </b-navbar-nav>
        <!-- right navbar item -->
        <!-- jika belum login -->
        <b-navbar-nav v-if="!this.$auth.loggedIn" class="ml-auto">
          <router-link class="ml-2" to="/login">
            <b-button variant="success">Login</b-button>
          </router-link>
          <router-link class="ml-2" to="/register">
            <b-button variant="danger">Register</b-button>
          </router-link>
        </b-navbar-nav>

        <!-- jika sudah login -->
        <b-navbar-nav v-else class="ml-auto">
          <div class="ml-2 mt-2">{{ this.$auth.user.email }}</div>
          <b-button class="ml-2" variant="danger" @click="$auth.logout()"
            >Logout</b-button
          >
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>
    <nuxt />
  </div>
</template>

<script>
export default {
  methods: {
    async logout() {
      await this.$auth.logout()
    }
  }
}
</script>
<style>
html {
  font-family: 'Source Sans Pro', -apple-system, BlinkMacSystemFont, 'Segoe UI',
    Roboto, 'Helvetica Neue', Arial, sans-serif;
  font-size: 16px;
  word-spacing: 1px;
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
  box-sizing: border-box;
}

*,
*:before,
*:after {
  box-sizing: border-box;
  margin: 0;
}

.button--green {
  display: inline-block;
  border-radius: 4px;
  border: 1px solid #3b8070;
  color: #3b8070;
  text-decoration: none;
  padding: 10px 30px;
}

.button--green:hover {
  color: #fff;
  background-color: #3b8070;
}

.button--grey {
  display: inline-block;
  border-radius: 4px;
  border: 1px solid #35495e;
  color: #35495e;
  text-decoration: none;
  padding: 10px 30px;
  margin-left: 15px;
}

.button--grey:hover {
  color: #fff;
  background-color: #35495e;
}
</style>
