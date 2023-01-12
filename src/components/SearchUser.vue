<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <p>
      You can view the list of
      <a href="https://https://github.com/" target="_blank" rel="noopener"
        >GitHub</a
      >
      user repositories by typing username.
    </p>

    <h3>Type in username</h3>
    <input v-model="username" @keyup.enter="searchUser()" class="search" />
    <button @click="searchUser()" class="search-button">Search</button>
    <br />
    <span v-if="usernameSearched && !userExists"
      >User {{ usernameSearched }} does not exist.</span
    >

    <div v-if="userExists">
      <h3>Repositories owned by {{ usernameSearched }}</h3>
      <p v-if="repos.length == 0">
        User {{ usernameSearched }} does not own any repositories.
      </p>
      <ReposTable :repos="repos.slice(0, 5)" />
    </div>

    <div v-if="repos.length > 5">
      <h3>Do you want to see the other {{ repos.length - 5 }} repos?</h3>
      <router-link :to="{ name: 'all', params: { repos } }"
        >See all repos</router-link
      >
    </div>
  </div>
</template>

<script>
import ReposTable from "@/components/ReposTable.vue";

export default {
  name: "SearchUser",
  components: {
    ReposTable,
  },
  props: {
    msg: String,
  },
  data() {
    return {
      username: "",
      usernameSearched: "",
      userExists: false,
      repos: [],
    };
  },
  methods: {
    async searchUser() {
      this.usernameSearched = "";
      const response = await fetch(
        `https://api.github.com/users/${this.username}/repos`
      );
      if (response.status === 200) {
        this.userExists = true;
        this.repos = await response.json();
      } else if (response.status === 404) {
        this.userExists = false;
      }
      this.usernameSearched = this.username;
      this.username = "";
    },
  },
};
</script>

<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
table {
  border-collapse: collapse;
  margin: 25px 0;
  font-size: 0.9em;
  min-width: 400px;
  box-shadow: 0 0 20px rgba(0, 0, 0, 0.15);
  margin-left: auto;
  margin-right: auto;
}
table thead tr {
  background-color: #42b983;
  color: #ffffff;
  text-align: left;
}
table th,
table td {
  padding: 12px 15px;
}
table tbody tr {
  border-bottom: 1px solid #dddddd;
}
table tbody tr:nth-of-type(even) {
  background-color: #f3f3f3;
}
.search {
  margin: 5px 0;
  font-family: sans-serif;
}
.search-button {
  margin: 5px 0;
  font-family: sans-serif;
  background-color: #42b983;
  border-color: #42b983;
}
</style>
