<template>
  <div v-if="repos" class="about">
    <h3>All repos owned by {{ user }}</h3>
    <ReposTable :repos="repos" />
    <router-link :to="{ name: 'home', params: { user } }">Go back</router-link>
  </div>
  <div v-else class="about">
    <h1>No repos yet!</h1>
    <h1>Go back <router-link to="/">Home</router-link> and search for user</h1>
  </div>
</template>

<script>
import ReposTable from "@/components/ReposTable.vue";

export default {
  components: {
    ReposTable,
  },
  data() {
    return {
      repos: this.$route.params.repos,
      user: "",
    };
  },
  async created() {
    if (this.repos !== undefined) {
      this.user = this.repos[0].owner.login;
    }
  },
};
</script>

<style scoped>
.a.router-link-active:visited {
  color: #42b983;
}
</style>
