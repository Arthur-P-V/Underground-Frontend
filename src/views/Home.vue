<template>
  <div class="home">
    <h1>Underground</h1>
    <!-- <h2>{{ category }}</h2> -->
    <button v-on:click="indexCategory">All</button>
    <button v-on:click="gamesCategory">Games</button>
    <button v-on:click="musicCategory">Music</button>
    <button v-on:click="moviesCategory">Movies</button>
    <div v-for="post in filterBy(posts, `${category}`, 'category')" :key="post.id">
      <router-link :to="`/posts/${post.id}`">
        <h1>{{ post.title }}</h1>
        <router-link :to="`/users/${post.user.id}`">
          <h3>{{ post.user.name }}</h3>
        </router-link>
        <h4>{{ post.category }}</h4>
        <h5>{{ post.score }}</h5>
        <p>{{ post.content }}</p>
      </router-link>
    </div>
  </div>
</template>

<style></style>

<script>
import axios from "axios";
import Vue2Filters from "vue2-filters";

export default {
  mixins: [Vue2Filters.mixin],
  data: function() {
    return {
      posts: [],
      // eslint-disable-next-line prettier/prettier
      category: '',
      check: "",
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
    gamesCategory: function() {
      // eslint-disable-next-line prettier/prettier
      this.category = 'Games';
    },
    indexCategory: function() {
      // eslint-disable-next-line prettier/prettier
      this.category = ''
    },
    musicCategory: function() {
      // eslint-disable-next-line prettier/prettier
      this.category = 'Music'
    },
    moviesCategory: function() {
      // eslint-disable-next-line prettier/prettier
      this.category = 'Movies'
    },
  },
};
</script>
