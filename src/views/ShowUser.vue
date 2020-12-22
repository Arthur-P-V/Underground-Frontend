<template>
  <div>
    <h1>{{ user.username }}</h1>
    <h2>Post Count: {{ user.total_posts }}</h2>
    <h2>Comment Count: {{ user.total_comments }}</h2>
    <div v-for="post in user.posts" :key="post.id">
      <router-link :to="`/posts/${post.id}`">
        <h3>{{ post.title }}</h3>
      </router-link>
    </div>
  </div>
</template>
<script>
import axios from "axios";

export default {
  data: function() {
    return {
      user: {},
    };
  },
  created: function() {
    axios.get("/api/users/" + this.$route.params.id).then(response => {
      console.log("success", response.data);
      this.user = response.data;
    });
  },
};
</script>
