<template>
  <div>
    <h1>ini id : {{ id }}</h1>
  </div>
</template>
<script>
export default {
  data() {
    return {
      id: 0
    }
  },
  mounted() {
    this.getId()
  },

  methods: {
    getId() {
      this.id = this.$route.params.id
    }
  }
}
</script>
