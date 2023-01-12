<template>
  <div v-if="repos" class="about">
    <ReposTable :repos="repos" />
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
    };
  },
  methods: {
    created() {
      console.log("log", this.repos);
    },
  },
};
</script>
<style scoped>
.a.router-link-active:visited {
  color: #42b983;
}
</style>
