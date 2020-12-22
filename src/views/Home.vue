<template>
  <div class="home">
    <h1>Underground</h1>
    <div v-for="post in posts" :key="post.id">
      <router-link :to="`/posts/${post.id}`">
        <h1>{{ post.title }}</h1>
        <router-link :to="`/users/${post.user.id}`">
          <h3>{{ post.user.name }}</h3>
        </router-link>
        <h4>{{ post.score }}</h4>
        <p>{{ post.content }}</p>
      </router-link>
    </div>
  </div>
</template>

<style></style>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      posts: [],
    };
  },
  created: function() {
    this.indexPosts();
  },
  methods: {
    indexPosts: function() {
      axios.get("/api/posts").then(response => {
        console.log("Success", response.data);
        this.posts = response.data;
      });
    },
  },
};
</script>
