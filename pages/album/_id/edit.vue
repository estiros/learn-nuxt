<template>
  <b-container>
    <center>
      <h1>Form Edit</h1>
    </center>
    <b-form @submit="simpan">
      <b-form-input
        v-model="user_id"
        class="mb-2"
        type="number"
        placeholder="User ID"
        required
        min="0"
      />
      <b-form-input
        v-model="judul"
        class="mb-2"
        type="text"
        placeholder="Title"
        required
      />
      <div class="row">
        <router-link to="/album" class="ml-3 mr-3">
          <b-button>Cancel</b-button>
        </router-link>
        <b-button variant="success" type="submit">Save</b-button>
      </div>
    </b-form>
  </b-container>
</template>

<script>
import axios from 'axios'
export default {
  data() {
    return {
      user_id: '',
      judul: ''
    }
  },
  mounted() {
    this.getData()
  },
  methods: {
    async getData() {
      const res = await axios.get(
        `http://localhost:3001/albums/${this.$route.params.id}`
      )
      // eslint-disable-next-line no-console
      console.log(res)
      this.user_id = res.data.userId
      this.judul = res.data.title
    },
    simpan(evt) {
      evt.preventDefault()
      axios
        .patch(`http://localhost:3001/albums/${this.$route.params.id}`, {
          userId: this.user_id,
          title: this.judul // yg di api : v-model
        })
        .then((res) => {
          // console.log('hasilnya: ', res)
          alert(JSON.stringify(this.user_id + ' ' + this.judul))
          this.$router.push('/album')
        })
      // method post ada tiga url, body, header
    }
  }
}
</script>

<style></style>
