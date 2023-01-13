<template>
  <div v-if="repo[0]" class="about">
    <h3>Details of {{ repo[0].name }} owned by {{ user }}</h3>
    <ReposTable :repos="repo" :mode="mode" :repoDetails="repoDetails" />
    <router-link :to="{ name: 'home', params: { user } }">Go back</router-link>
  </div>
  <div v-else class="about">
    <h1>No repos yet!</h1>
    <h1>Go back <router-link to="/">Home</router-link> and search for user</h1>
  </div>
</template>

<script>
import ReposTable from "@/components/ReposTable.vue";
import * as consts from "@/consts.js";

export default {
  components: {
    ReposTable,
  },
  data() {
    return {
      repo: [this.$route.params.repo],
      mode: consts.TABLE_MODE_DETAIL,
      repoDetails: { commits: null, comments: null, stargazers: null },
      user: "",
    };
  },
  methods: {
    async fetchRepoDetails(property) {
      const repoName = this.repo[0].name;
      const ownerName = this.repo[0].owner.login;
      const response = await fetch(
        ` https://api.github.com/repos/${ownerName}/${repoName}/${property}`
      );
      if (response.status === 200) {
        const commits = await response.json();
        this.repoDetails[property] = commits.length;
      } else if (response.status === 404) {
        this.repoDetails[property] = "n/a";
      }
    },
  },
  async created() {
    if (this.repo[0] !== undefined) {
      this.user = this.repo[0].owner.login;
      for (const property of ["commits", "comments", "stargazers"]) {
        await this.fetchRepoDetails(property);
      }
    }
  },
};
</script>
