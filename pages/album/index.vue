<template>
  <b-container>
    <center>
      <h1 class="mb-5 mt-3">Ini Album</h1>
    </center>
    <div class="row mb-2">
      <div class="col-md-6">
        <router-link to="/album/create">
          <b-button variant="warning">Create</b-button>
        </router-link>
      </div>
      <div class="col-md-4">
        <div class="row">
          <b-input v-model="textSearch" class="col-xs-6 col-sm-8 col-md-9 " />
          <div class="col-xs-6 col-sm-4 col-md-3 ">
            <b-button @click="search">Search</b-button>
          </div>
        </div>
      </div>
      <div class="col-md-2">
        <!-- Buat Filter -->
        <b-dropdown id="dropdown-1" text="Filter by UserID" variant="primary">
          <b-dropdown-item v-for="n in 10" :key="n" @click="filter(n)"
            >UserID {{ n }}</b-dropdown-item
          >
        </b-dropdown>
      </div>
    </div>

    <b-table-simple hover small caption-top responsive>
      <b-thead>
        <b-th class="text-center">User ID</b-th>
        <b-th class="text-center">ID</b-th>
        <b-th class="text-center">Title</b-th>
        <b-th class="text-center">Action</b-th>
      </b-thead>
      <b-tbody>
        <ListItemAlbum
          v-for="item in albums"
          :key="item.id"
          :album="item"
          @refresh-table="getData"
        />
        <!-- <tr v-for="item in album" :key="item.id">
          <td>{{ item.userId }}</td>
          <td>{{ item.id }}</td>
          <td>{{ item.title }}</td>
        </tr>-->
      </b-tbody>
    </b-table-simple>
  </b-container>
</template>

<script>
// import axios from 'axios'
import ListItemAlbum from '../../components/list-item-album'

export default {
  components: { ListItemAlbum },
  data() {
    return {
      albums: [],
      textSearch: ''
    }
  },
  mounted() {
    this.getData()
  },
  methods: {
    getData() {
      this.$axios
        .get('albums')
        .then((res) => {
          this.albums = res.data
          // console.log(res)
        })
        .catch((err) => {
          // eslint-disable-next-line no-console
          console.error(err)
        })
    },
    async search() {
      const res = await this.$axios.get(`albums?q=${this.textSearch}`)
      this.albums = res.data
    },
    async filter(n) {
      const res = await this.$axios.get(`albums?userId=${n}`)
      this.albums = res.data
    }
  }
}
</script>
