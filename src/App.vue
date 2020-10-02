<template>
<div class="wrapper">

  <header>
    <h1>header</h1>

    <div class="container">
      <nav class="navbar">
        <div class="navbar-content">
          <div class="logo">Github Finder</div>
          <!-- <ul class="navbar-list">
            <li class="navbar-item" v-for="link in links" :key="link.title">
              <router-link
                class="navbar-link"
                :title="link.title"
                :to="link.url">
                  {{  link.title}}
                </router-link>
            </li>
          </ul> -->
        </div>
      </nav>
    </div>
  </header>

  <router-view></router-view>

  <footer></footer>

</div>
</template>

<script>

export default {
  data() {
    return {
      // создаём массив с содержимым ссылок
      links: [
        {title: 'Home', url: '/'},
      ]
    }
  },
}
</script>

<style lang="scss">
  .navbar-link {
    &.router-link-exact-active {
      color: #5247e7;
    }
  }
</style>