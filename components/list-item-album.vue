<template>
  <b-tr>
    <b-td class="text-center">{{ album.userId }}</b-td>
    <b-td class="text-center">{{ album.id }}</b-td>
    <b-td>{{ album.title }}</b-td>
    <b-td class="text-center">
      <div>
        <b-button v-b-modal="`my-modal-${album.id}`" variant="primary"
          >View</b-button
        >
        <router-link :to="`/album/${album.id}/edit`">
          <b-button variant="success">Edit</b-button>
        </router-link>
        <b-button variant="danger" @click="deleteButton">Delete</b-button>

        <!-- The modal -->
        <b-modal
          :id="`my-modal-${album.id}`"
          size="lg"
          ok-only="true"
          hide-header-close="true"
        >
          <table>
            <tr>
              <td>ID</td>
              <td>:</td>
              <td>{{ album.id }}</td>
            </tr>
            <tr>
              <td>User ID</td>
              <td>:</td>
              <td>{{ album.userId }}</td>
            </tr>
            <tr>
              <td>Title</td>
              <td>:</td>
              <td>{{ album.title }}</td>
            </tr>
          </table>
        </b-modal>
      </div>
    </b-td>
  </b-tr>
</template>

<script>
import axios from 'axios'
export default {
  // eslint-disable-next-line vue/require-prop-types
  props: ['album'],
  methods: {
    async deleteButton() {
      // eslint-disable-next-line no-use-before-define
      const setuju = confirm('Are you sure want to delete this data?')
      if (setuju) {
        await axios.delete('http://localhost:3001/albums/' + this.album.id)
        // await this.$axios.delete(`albums/${this.album.id}`)
        this.$emit('refresh-table')
      } else {
      }

      // this.$router.go('album')
    }
  }
}
</script>
