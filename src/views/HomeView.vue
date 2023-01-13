<template>
  <div class="home">
    <SearchUser msg="Welcome to my GitHub App!" :user="user" />
  </div>
</template>

<script>
import SearchUser from "@/components/SearchUser.vue";

export default {
  name: "HomeView",
  components: {
    SearchUser,
  },
  data() {
    return {
      user: this.$route.params.user,
    };
  },
};
</script>
