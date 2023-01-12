<template>
  <div v-if="repo[0].name" class="about">
    <ReposTable :repos="repo" :mode="mode" />
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
      repoDetails: { commits: null, comments: null, stars: null },
    };
  },
  methods: {
    created() {
      console.log("log", this.repo);
    },
    // fetchRepoDetails(repo) {
    //   // const repoName = repo[0].name;
    //   // const ownerName = repo[0].owner.login;
    //   // response = await fetch(`https://api.github.com/users/${USERNAME}`)
    //   console.log("search", this.response.status === "200");
    //   if (this.response.status === "200") {
    //     // fetch repo
    //     // this.repos =
    //     // fetch commit, comment, stars = obiekt repoDetails
    //     this.userExists = true;
    //   } else if (this.response.status === "404") {
    //     this.msgAboutUser = `User ${this.username} does not exist.`;
    //     this.userExists = false;
    //   }
    // this.username = "";
    // },
  },
};
</script>
