<template>
  <div class="wrapper-content wrapper-content--fixed">
    <section>
      <div class="container">
        <h1>Home Page</h1>

        <Search
          :value="search"
          @search="search = $event"
          placeholder="Type username..."/>

          <button v-if="!repos" class="btn btnPrimary" @click="getRepos">Search</button>
          <button v-else class="btn btnPrimary" @click="getRepos">Search again!</button>

              <p v-if="noRepos" style="margin-top: 20px">{{ noReposTitle }}</p>

          <!-- errors -->
          <div class="error" v-if="error" style="margin-top: 20px; color: red">
            <p>{{ error }}</p>
          </div>

          <!-- repos wrapper -->
          <div class="repos repos__wrapper" v-if="repos">
            <!-- repos item from array -->
            <div class="repos__item" v-for="repo in repos" :key="repo.id">
              <div class="repos__info">
                <a class="repos__link" target="_blank" :href="repo.html_url">{{ repo.name }}</a>
                <span>{{ repo.stargazers_count }} ⭐</span>
              </div>
            </div>
          </div>

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
      search: '',
      error: null,
      repos: null,
      noRepos: null,
      noReposTitle: 'User have 0 repos'
    }
  },
  methods: {
    getRepos () {
      // https://api.github.com/users/vedees/repos
      // console.log(`get user ${this.search}`)

      axios
        .get(`https://api.github.com/users/${this.search}/repos`)
        .then(res => {
          console.log(res)
          this.repos = res.data
          this.error = null
          this.noRepos = null

          if (res.data.length === 0) this.noRepos = true
        })
        .catch(err => {
          console.log(err)
          this.repos = null
          this.noRepos = null
          this.error = 'Can`t find this user'
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

  .repos {
    &__wrapper {
      width: 400px;
      margin: 30px 0;
    }
    &__info {
      display: flex;
      align-items: center;
      justify-content: space-between;
      margin-bottom: 10px;
      padding: 10px 0;
      border-bottom: 1px solid #dbdbdb;
    }
  }
</style>
