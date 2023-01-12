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
    <span>{{ msgAboutUser }}</span>
    <div v-if="userExists">
      <h3>Repositories owned by {{ username }}</h3>
      <p v-if="repos.length == 0">
        User {{ username }} does not own any repositories.
      </p>
      <ReposTable :repos="repos" />
    </div>
    <div v-if="repos.length > 3">
      <h3>Do you want to see the other {{ repos.length - 3 }} repos?</h3>
      <router-link :to="{ name: 'all', params: { repos } }"
        >See all repos</router-link
      >
    </div>
  </div>
</template>

<script>
import ReposTable from "@/components/ReposTable.vue";
// ReposTable: () => import("@/components/ReposTable.vue"),

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
      response: { status: "200" },
      msgAboutUser: "",
      userExists: false,
      repos: [
        {
          id: 1296269,
          node_id: "MDEwOlJlcG9zaXRvcnkxMjk2MjY5",
          name: "Hello-World",
          full_name: "octocat/Hello-World",
          owner: {
            login: "octocat",
            id: 1,
            node_id: "MDQ6VXNlcjE=",
            avatar_url: "https://github.com/images/error/octocat_happy.gif",
            gravatar_id: "",
            url: "https://api.github.com/users/octocat",
            html_url: "https://github.com/octocat",
            repos_url: "https://api.github.com/users/octocat/repos",
            events_url: "https://api.github.com/users/octocat/events{/privacy}",
            received_events_url:
              "https://api.github.com/users/octocat/received_events",
            type: "User",
            site_admin: false,
          },
          private: false,
          html_url: "https://github.com/octocat/Hello-World",
          description: "This your first repo!",
          fork: false,
          url: "https://api.github.com/repos/octocat/Hello-World",
          archive_url:
            "https://api.github.com/repos/octocat/Hello-World/{archive_format}{/ref}",
          comments_url:
            "https://api.github.com/repos/octocat/Hello-World/comments{/number}",
          commits_url:
            "https://api.github.com/repos/octocat/Hello-World/commits{/sha}",
          compare_url:
            "https://api.github.com/repos/octocat/Hello-World/compare/{base}...{head}",
          contents_url:
            "https://api.github.com/repos/octocat/Hello-World/contents/{+path}",
          contributors_url:
            "https://api.github.com/repos/octocat/Hello-World/contributors",
          deployments_url:
            "https://api.github.com/repos/octocat/Hello-World/deployments",
          downloads_url:
            "https://api.github.com/repos/octocat/Hello-World/downloads",
          git_commits_url:
            "https://api.github.com/repos/octocat/Hello-World/git/commits{/sha}",
          git_refs_url:
            "https://api.github.com/repos/octocat/Hello-World/git/refs{/sha}",
          git_tags_url:
            "https://api.github.com/repos/octocat/Hello-World/git/tags{/sha}",
          git_url: "git:github.com/octocat/Hello-World.git",
          stargazers_url:
            "https://api.github.com/repos/octocat/Hello-World/stargazers",
          statuses_url:
            "https://api.github.com/repos/octocat/Hello-World/statuses/{sha}",
          subscribers_url:
            "https://api.github.com/repos/octocat/Hello-World/subscribers",
          subscription_url:
            "https://api.github.com/repos/octocat/Hello-World/subscription",
          tags_url: "https://api.github.com/repos/octocat/Hello-World/tags",
          teams_url: "https://api.github.com/repos/octocat/Hello-World/teams",
          trees_url:
            "https://api.github.com/repos/octocat/Hello-World/git/trees{/sha}",
          clone_url: "https://github.com/octocat/Hello-World.git",
          mirror_url: "git:git.example.com/octocat/Hello-World",
          hooks_url: "https://api.github.com/repos/octocat/Hello-World/hooks",
          svn_url: "https://svn.github.com/octocat/Hello-World",
          homepage: "https://github.com",
          language: null,
          forks_count: 9,
          stargazers_count: 80,
          watchers_count: 80,
          size: 108,
          default_branch: "master",
          open_issues_count: 0,
          is_template: false,
          topics: ["octocat", "atom", "electron", "api"],
          has_downloads: true,
          has_discussions: false,
          archived: false,
          disabled: false,
          visibility: "public",
          pushed_at: "2011-01-26T19:06:43Z",
          created_at: "2011-01-26T19:01:12Z",
          updated_at: "2011-01-26T19:14:43Z",
          permissions: {
            admin: false,
            push: false,
            pull: true,
          },
          security_and_analysis: {
            advanced_security: {
              status: "enabled",
            },
            secret_scanning: {
              status: "enabled",
            },
            secret_scanning_push_protection: {
              status: "disabled",
            },
          },
        },
        {
          id: 1296269,
          node_id: "MDEwOlJlcG9zaXRvcnkxMjk2MjY5",
          name: "Hello-World",
          full_name: "octocat/Hello-World",
          owner: {
            login: "octocat",
            id: 1,
            node_id: "MDQ6VXNlcjE=",
            avatar_url: "https://github.com/images/error/octocat_happy.gif",
            gravatar_id: "",
            url: "https://api.github.com/users/octocat",
            html_url: "https://github.com/octocat",
            repos_url: "https://api.github.com/users/octocat/repos",
            events_url: "https://api.github.com/users/octocat/events{/privacy}",
            received_events_url:
              "https://api.github.com/users/octocat/received_events",
            type: "User",
            site_admin: false,
          },
          private: false,
          html_url: "https://github.com/octocat/Hello-World",
          description: "This your first repo!",
          fork: false,
          url: "https://api.github.com/repos/octocat/Hello-World",
          archive_url:
            "https://api.github.com/repos/octocat/Hello-World/{archive_format}{/ref}",
          comments_url:
            "https://api.github.com/repos/octocat/Hello-World/comments{/number}",
          commits_url:
            "https://api.github.com/repos/octocat/Hello-World/commits{/sha}",
          compare_url:
            "https://api.github.com/repos/octocat/Hello-World/compare/{base}...{head}",
          contents_url:
            "https://api.github.com/repos/octocat/Hello-World/contents/{+path}",
          contributors_url:
            "https://api.github.com/repos/octocat/Hello-World/contributors",
          deployments_url:
            "https://api.github.com/repos/octocat/Hello-World/deployments",
          downloads_url:
            "https://api.github.com/repos/octocat/Hello-World/downloads",
          git_commits_url:
            "https://api.github.com/repos/octocat/Hello-World/git/commits{/sha}",
          git_refs_url:
            "https://api.github.com/repos/octocat/Hello-World/git/refs{/sha}",
          git_tags_url:
            "https://api.github.com/repos/octocat/Hello-World/git/tags{/sha}",
          git_url: "git:github.com/octocat/Hello-World.git",
          stargazers_url:
            "https://api.github.com/repos/octocat/Hello-World/stargazers",
          statuses_url:
            "https://api.github.com/repos/octocat/Hello-World/statuses/{sha}",
          subscribers_url:
            "https://api.github.com/repos/octocat/Hello-World/subscribers",
          subscription_url:
            "https://api.github.com/repos/octocat/Hello-World/subscription",
          tags_url: "https://api.github.com/repos/octocat/Hello-World/tags",
          teams_url: "https://api.github.com/repos/octocat/Hello-World/teams",
          trees_url:
            "https://api.github.com/repos/octocat/Hello-World/git/trees{/sha}",
          clone_url: "https://github.com/octocat/Hello-World.git",
          mirror_url: "git:git.example.com/octocat/Hello-World",
          hooks_url: "https://api.github.com/repos/octocat/Hello-World/hooks",
          svn_url: "https://svn.github.com/octocat/Hello-World",
          homepage: "https://github.com",
          language: null,
          forks_count: 9,
          stargazers_count: 80,
          watchers_count: 80,
          size: 108,
          default_branch: "master",
          open_issues_count: 0,
          is_template: false,
          topics: ["octocat", "atom", "electron", "api"],
          has_downloads: true,
          has_discussions: false,
          archived: false,
          disabled: false,
          visibility: "public",
          pushed_at: "2011-01-26T19:06:43Z",
          created_at: "2011-01-26T19:01:12Z",
          updated_at: "2011-01-26T19:14:43Z",
          permissions: {
            admin: false,
            push: false,
            pull: true,
          },
          security_and_analysis: {
            advanced_security: {
              status: "enabled",
            },
            secret_scanning: {
              status: "enabled",
            },
            secret_scanning_push_protection: {
              status: "disabled",
            },
          },
        },
        {
          id: 1296269,
          description: "MDEwOlJlcG9zaXRvcnkxMjk2MjY5",
          private: true,
          full_name: "octocat/Hello-World",
        },
        {
          id: 1296269,
          description: "MDEwOlJlcG9zaXRvcnkxMjk2MjY5",
          private: true,
          full_name: "octocat/Hello-World",
        },
        {
          id: 1296269,
          description: "MDEwOlJlcG9zaXRvcnkxMjk2MjY5",
          private: true,
          full_name: "octocat/Hello-World",
        },
      ],
    };
  },
  methods: {
    searchUser() {
      // response = await fetch(`https://api.github.com/users/${USERNAME}`)
      console.log("search", this.response.status === "200");
      if (this.response.status === "200") {
        // fetch repo
        // this.repos =
        // fetch commit, comment, stars = obiekt repoDetails
        this.userExists = true;
      } else if (this.response.status === "404") {
        this.msgAboutUser = `User ${this.username} does not exist.`;
        this.userExists = false;
      }
      // this.username = "";
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
