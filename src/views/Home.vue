<template>
  <div class="home">
    <!-- <h2>{{ category }}</h2> -->
    <div class="main">
      <div
        class="page-header largest parallax custom text-center"
        v-bind:style="`background-image:url(assets/images/page-header-bg.jpg)`"
        data-0="background-position:50% 50%;"
        data-top-bottom="background-position:50% 100%"
      >
        <div class="container-fluid">
          <h1 data-300-top="opacity:1;transform:scale(1);" data-top-bottom="opacity:0.4;transform:scale(1.9);">Blog</h1>
          <ol class="breadcrumb" data-300-top="opacity:1;" data-top-bottom="opacity:0.4;">
            <li><a href="index.html">Home</a></li>
            <li><a href="#">Pages</a></li>
            <li class="active">Blog</li>
          </ol>
        </div>
        <!-- End .container-fluid -->
      </div>
      <!-- End .page-header -->

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
          <div id="blog-item-container" class="max-col-2" data-layoutmode="fitRows">
            <div v-for="post in filterBy(posts, `${category}`, 'category')" :key="post.id">
              <article class="entry entry-grid">
                <div class="entry-media">
                  <figure>
                    <a href="single.html"><img v-bind:src="post.image_url" alt="Post image" /></a>
                  </figure>
                </div>
                <!-- End .entry-media -->

                <!-- <div class="entry-icon">
                <i class="fa fa-file-image-o"></i>
              </div> -->
                <!-- End .entry-icon -->

                <div class="entry-content-container">
                  <!-- <div class="entry-meta">
                  <div>
                    <i class="fa fa-calendar"></i>
                    17 Aug 2016
                  </div>
                  <div>
                    <a href="#">
                      <i class="fa fa-comments"></i>
                      8 Comment(s)
                    </a>
                  </div>
                </div> -->
                  <!-- End .entry-meta -->

                  <div class="entry-content-wrapper">
                    <h2 class="entry-title">
                      {{ post.title }}
                    </h2>
                    <div class="entry-content">
                      <p>
                        {{ post.content }}
                      </p>
                      <a v-bind:href="`/posts/${post.id}`" class="readmore">
                        Read more
                        <i class="fa fa-angle-right"></i>
                      </a>
                    </div>
                    <!-- End .entry-content -->
                  </div>
                  <!-- End .entry-content-wrapper -->
                </div>
                <!-- End .entry-content-container -->
              </article>
              <!-- <router-link :to="`/posts/${post.id}`">
              <h2>{{ post.title }}</h2>
              <router-link :to="`/users/${post.user.id}`">
                <h3>{{ post.user.name }}</h3>
              </router-link>
              <h4>{{ post.category }}</h4>
              <h5>{{ post.score }}</h5>
              <p>{{ post.content }}</p>
            </router-link> -->
            </div>
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
