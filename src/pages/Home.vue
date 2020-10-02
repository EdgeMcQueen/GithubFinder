<template>
  <div class="wrapper-content wrapper-content--fixed">
    <section>
      <div class="container">
        <h1>Home Page</h1>

        <Search
          :value="search"
          @search="search = $event"
          placeholder="Type username..."/>

          <button class="btn btnPrimary" @click="getRepos">Search</button>

      </div>
    </section>
  </div>
</template>

<script>
import Search from '@/components/Search.vue';
import axios from 'axios'


export default {
  components: {
    Search,
  },
  data() {
    return {
      search: ''
    }
  },
  methods: {
    getRepos () {
      // https://api.github.com/users/vedees/repos
      console.log(`get user ${this.search}`)

      axios
        .get(`https://api.github.com/users/${this.search}/repos`)
        .then(res => {
          console.log(res)
        })
        .catch(err => {
          console.log(err)
        })
    }
  },
}
</script>

<style lang="scss" scoped>
  .container {
    display: flex;
    align-items: center;
    flex-direction: column;
  }

  .btn {
    margin-top: 40px;
  }
</style>
