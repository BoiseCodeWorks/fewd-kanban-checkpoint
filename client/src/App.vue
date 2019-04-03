<template>
  <div id="app">
    <div v-if="user._id" class="px-3 mb-3 d-flex justify-content-between align-items-center my-shadow">
      <img @click="$router.push({name: 'boards'})" class="action" height="75px" src="https://www.riteaid.com/shop/media/catalog/product/cache/1/image/9df78eab33525d08d6e5fb8d27136e95/0/2/021200474019_1.jpg" alt="logo">
      <button @click="logout">Logout</button>
    </div>
    <router-view />
  </div>
</template>

<script>
  export default {
    name: 'App',
    computed: {
      user() {
        return this.$store.state.user
      }
    },
    methods: {
      logout() {
        this.$store.dispatch('logout')
      }
    }
  }
</script>

<style>
  #app {
    font-family: "Avenir", Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
  }

  #nav {
    padding: 30px;
  }

  #nav a {
    font-weight: bold;
    color: #2c3e50;
  }

  #nav a.router-link-exact-active {
    color: #42b983;
  }
  .action {
    cursor: pointer;
  }
  .my-shadow {
    box-shadow: 0 0 5px 1px black;
  }
</style>