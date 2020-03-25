<template>
  <div>
    <h1>ini id : {{ data.id }}</h1>
    <p>User ID: {{ data.userId }}</p>
    <p>Title: {{ data.title }}</p>
    <router-link :to="'/album/'">
      <b-button variant="primary">Back</b-button>
    </router-link>
  </div>
</template>
<script>
export default {
  data() {
    return {
      id: 0,
      data: {}
    }
  },
  mounted() {
    this.getId()
    this.getData()
  },

  methods: {
    getId() {
      this.id = this.$route.params.id
    },
    async getData() {
      const res = await this.$axios.get('albums/' + this.$route.params.id)
      this.data = res.data
    }
    // getData() {
    //   this.$axios
    //     .get('albums/' + this.$route.params.id)
    //     .then((res) => {
    //       this.data = res.data
    //     })
    //     .catch((err) => {
    //       // eslint-disable-next-line no-console
    //       console.error(err)
    //     })
    // }
  }
}
</script>
