<template>
  <div class="hello">
    <table id="firstTable">
      <thead>
        <tr>
          <th>Name</th>
          <th>Access</th>
          <th>Go to repo</th>
          <th>{{ isGeneralMode ? "See details" : "Commits" }}</th>
          <th v-if="!isGeneralMode">Comments</th>
          <th v-if="!isGeneralMode">Stars</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(repo, index) in repos" :key="index">
          <td>{{ repo.name }}</td>
          <td>{{ repo.private ? "Private" : "Public" }}</td>
          <td>
            <a :href="repo.html_url" target="_blank" rel="noopener"
              >Go to repo</a
            >
          </td>
          <td v-if="isGeneralMode">
            <router-link :to="{ name: 'details', params: { repo } }"
              >See details</router-link
            >
          </td>
          <td v-if="!isGeneralMode && repoDetails">
            {{ repoDetails.commits }}
          </td>
          <td v-if="!isGeneralMode && repoDetails">
            {{ repoDetails.comments }}
          </td>
          <td v-if="!isGeneralMode && repoDetails">{{ repoDetails.stars }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import * as consts from "@/consts.js";

export default {
  name: "ReposTable",
  props: {
    repos: Array,
    mode: {
      type: String,
      default: consts.TABLE_MODE_GENERAL,
    },
    repoDetails: {
      type: Object,
      required: false,
    },
  },
  data() {
    return {
      generalMode: consts.TABLE_MODE_GENERAL,
      detailMode: consts.TABLE_MODE_DETAIL,
    };
  },
  computed: {
    isGeneralMode: function () {
      console.log("mode", this.mode === this.generalMode);
      return this.mode === this.generalMode;
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
