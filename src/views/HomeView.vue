<template>
  <div class="home">
    <SearchUser msg="Welcome to my GitHub App!" />
  </div>
</template>

<script>
import SearchUser from "@/components/SearchUser.vue";

export default {
  name: "HomeView",
  components: {
    SearchUser,
  },
};
</script>
