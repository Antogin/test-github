<template>
  <div id="nav">
    <form v-on:submit.prevent="search">
      <input v-model="username" type="text" />
    </form>
  </div>
  <router-view />
</template>


<script>
export default {
  data: () => {
    return { name: "Shawn" };
  },
  methods: {
    search: function () {
      console.log('search', this.username)
      this.$router.push(this.username)

    },
  },
  mounted: async function () {
    this.name = "Shawn's Name"; // MAGIC
  },
};
</script>


<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
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
</style>
