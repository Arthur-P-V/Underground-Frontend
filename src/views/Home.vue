<template>
  <div class="home">
    <!-- <h2>{{ category }}</h2> -->
    <div class="main">
      <div class="container-fluid">
        <ul id="portfolio-filter">
          <li class="active"><a v-on:click="indexCategory">All</a></li>
          <li><a v-on:click="gamesCategory">Games</a></li>
          <li><a v-on:click="moviesCategory">Movies</a></li>
          <li><a v-on:click="musicCategory">Music</a></li>
        </ul>
      </div>
      <!-- <button v-on:click="indexCategory">All</button>
      <button v-on:click="gamesCategory">Games</button>
      <button v-on:click="musicCategory">Music</button>
      <button v-on:click="moviesCategory">Movies</button> -->
      <div class="container-fluid">
        <div class="blog-row">
          <div
            id="blog-item-container"
            class="col-12 col-lg-6 my-4"
            data-layoutmode="fitRows"
            v-for="post in filterBy(posts, `${category}`, 'category')"
            :key="post.id"
          >
            <article class="entry entry-grid">
              <div class="entry-media post-image">
                <figure>
                  <a v-bind:href="`/posts/${post.id}`"><img v-bind:src="post.image_url" alt="Post image" /></a>
                </figure>
              </div>
              <!-- End .entry-media -->
              <div class="entry-content-container">
                <div class="entry-content-wrapper">
                  <h2 class="entry-title">
                    {{ post.title }}
                  </h2>
                  <div class="entry-content">
                    <p>{{ post.user.name }}</p>
                    <a v-bind:href="`/posts/${post.id}`" class="readmore">
                      Read
                      <i class="fa fa-angle-right"></i>
                    </a>
                  </div>
                  <!-- End .entry-content -->
                </div>
                <!-- End .entry-content-wrapper -->
              </div>
              <!-- End .entry-content-container -->
            </article>
          </div>
        </div>
      </div>
      <div class="pagination-wrapper">
        <nav class="pagination-container">
          <label>Showing: 1-4 of 16</label>
          <ul class="pagination">
            <li class="active"><a href="#">1</a></li>
            <li><a href="#">2</a></li>
            <li><a href="#">3</a></li>
            <li><a href="#">4</a></li>
            <li>
              <a href="#" aria-label="Next">
                <span aria-hidden="true"><i class="fa fa-angle-right"></i></span>
              </a>
            </li>
          </ul>
        </nav>
      </div>
      <!-- End .pagination-wrapper -->
    </div>
  </div>
</template>

<style>
h1 {
  text-align: center;
}
.entry-media.post-image {
  width: 650px;
  max-height: 325px;
}
</style>

<script>
import axios from "axios";
import Vue2Filters from "vue2-filters";

export default {
  mixins: [Vue2Filters.mixin],
  data: function() {
    return {
      posts: [],
      // eslint-disable-next-line prettier/prettier
      category: "",
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
      this.category = "Games";
    },
    indexCategory: function() {
      // eslint-disable-next-line prettier/prettier
      this.category = "";
    },
    musicCategory: function() {
      // eslint-disable-next-line prettier/prettier
      this.category = "Music";
    },
    moviesCategory: function() {
      // eslint-disable-next-line prettier/prettier
      this.category = "Movies";
    },
  },
};
</script>
