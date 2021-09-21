<template>
  <div v-if="userData?.name" class="card">
    <img :src="userData.avatar_url" alt="John" style="width: 100%" />
    <h1>{{ userData.name }}</h1>
    <p class="title">{{ userData.bio }}</p>
    <p>Public repos: {{ userData.public_repos }}</p>

    <p><a :href="html_url" target="_blank">View</a></p>
  </div>
</template>



<script>
// @ is an alias to /src

export default {
  name: "Profile",
  data: function () {
    return {
      userData: null,
    };
  },
  watch: {
    "$route.params.username": function (username) {
      console.log("username", username);
      this.getUser();
    },
  },
  mounted() {
    this.getUser();
    this.username = this.$route.params.username;
  },
  methods: {
    getUser() {
      this.userData = null;
      const user = "antogin";

      const token = "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";
      const creds = `${user}:${token}`;

      const auth = btoa(creds);
      const options = {
        mode: "cors",
        headers: {
          Authorization: "Basic " + auth,
        },
      };

      console.log("$route.params.username", this.$route.params.username);
      fetch(
        `https://api.github.com/users/${this.$route.params.username}`,
        options
      )
        .then((resp) => {
          return resp.json();
        })
        .then((data) => {
          console.log("data", data);
          this.userData = data;
        });
    },
  },
};
</script>


<style scoped>
.card {
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
  max-width: 300px;
  margin: auto;
  text-align: center;
  font-family: arial;
}

.title {
  color: grey;
  font-size: 18px;
}

a {
  border: none;
  outline: 0;
  display: inline-block;
  color: white;
  background-color: #000;
  text-align: center;
  cursor: pointer;
  width: 100%;
  font-size: 18px;
}

button:hover,
a:hover {
  opacity: 0.7;
}
</style>