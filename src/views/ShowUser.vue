<template>
  <div>
    <!-- <img v-bind:src="user.profile_pic" v-bind:alt="user.name" />
    <h1>{{ user.username }}</h1>
    <h2 v-if="user.bio">Bio: {{ user.bio }}</h2>
    <h2>Post Count: {{ user.total_posts }}</h2>
    <h2>Comment Count: {{ user.total_comments }}</h2>
    <h3 v-if="user.fav_game">Favorite Game: {{ user.fav_game }}</h3>
    <h3 v-if="user.fav_movie">Favorite Movie: {{ user.fav_movie }}</h3>
    <h3 v-if="user.fav_band">Favorite Band: {{ user.fav_band }}</h3>
    <div v-for="post in user.posts" :key="post.id">
      <router-link :to="`/posts/${post.id}`">
        <h3>{{ post.title }}</h3>
      </router-link>
    </div>
    <button v-if="owner" v-on:click="editUser">Edit Profile</button>
    <dialog id="edit-user">
      <form method="dialog">
        <h1>Edit!</h1>
        <p>
          Name:
          <input type="text" v-model="user.name" />
        </p>
        <p>
          Email:
          <input type="text" v-model="user.email" />
        </p>
        <p>
          Profile Picture:
          <input type="text" v-model="user.profile_pic" />
        </p>
        <p>
          Bio:
          <input type="text" v-model="user.bio" />
        </p>
        <p>
          Favorite Game:
          <input type="text" v-model="user.fav_game" />
        </p>
        <p>
          Favorite Movie:
          <input type="text" v-model="user.fav_movie" />
        </p>
        <p>
          Favorite Band:
          <input type="text" v-model="user.fav_band" />
        </p>
        <button v-on:click="updateUser">Update</button>
        <button>close</button>
      </form>
    </dialog> -->
    <div class="table-row">
      <div
        class="table-cell cell-image smaller overlay-container"
        v-bind:style="`background-image:url(${user.profile_pic})`"
      ></div>
      <!-- End .table-cell -->
      <div class="table-cell cell-content larger bg-dark border text-muted">
        <div class="table-cell-wrapper">
          <header class="title-block mb35">
            <h2 class="title custom2 text-white">
              Account |
              <span class="light text-custom">{{ user.username }}</span>
            </h2>
          </header>
          <div class="row">
            <div class="col-xs-6 col-xss-12">
              <div class="aboutme-section">
                <h4 class="text-white">
                  Bio
                </h4>
                <p>
                  {{ user.bio }}
                </p>
              </div>
              <!-- End .aboutme-section -->
            </div>
            <!-- End .col-xs-6 -->

            <div class="col-xs-6 col-xss-12">
              <div class="aboutme-section">
                <h4 class="text-white">
                  Favorite Game
                </h4>
                <p>
                  {{ user.fav_game }}
                </p>
              </div>
              <!-- End .aboutme-section -->
            </div>
            <!-- End .col-xs-6 -->
          </div>
          <!-- End .row -->

          <div class="mb10"></div>
          <!-- margin -->

          <div class="row">
            <div class="col-xs-6 col-xss-12">
              <div class="aboutme-section">
                <h4 class="text-white">
                  Favorite Movie
                </h4>
                <p>
                  {{ user.fav_movie }}
                </p>
              </div>
              <!-- End .aboutme-section -->
            </div>
            <!-- End .col-xs-6 -->

            <div class="col-xs-6 col-xss-12">
              <div class="aboutme-section">
                <h4 class="text-white">
                  Favorite Band
                </h4>
                <p>
                  {{ user.fav_band }}
                </p>
              </div>
              <!-- End .aboutme-section -->
            </div>
            <!-- End .col-xs-6 -->
          </div>
          <!-- End .row -->

          <div class="mb10"></div>
          <!-- margin -->

          <div class="row">
            <div class="col-xs-6 col-xss-12">
              <div class="aboutme-section">
                <h4 class="text-white">
                  Total Posts
                </h4>
                <p>
                  {{ user.total_posts }}
                </p>
              </div>
              <!-- End .aboutme-section -->
            </div>
            <!-- End .col-xs-6 -->

            <div class="col-xs-6 col-xss-12">
              <div class="aboutme-section">
                <h4 class="text-white">
                  Total Comments
                </h4>
                <p>
                  {{ user.total_comments }}
                </p>
              </div>
              <!-- End .aboutme-section -->
            </div>
            <!-- End .col-xs-6 -->
          </div>
          <!-- End .row -->
        </div>
        <!-- End .table-cell-wrapper -->
        <!-- <a v-if="owner" v-on:click="editUser" class="btn btn-custom">Edit Profile</a> -->
        <button v-if="owner" class="btn btn-custom" data-toggle="modal" data-target="#modal-login-form">
          Edit Account
        </button>
        <div
          class="modal fade"
          id="modal-login-form"
          tabindex="-1"
          role="dialog"
          aria-labelledby="myModalLabel1"
          aria-hidden="true"
        >
          <form id="login-form" method="get">
            <div class="modal-dialog modal-sm">
              <div class="modal-content">
                <div class="modal-header">
                  <button type="button" class="close" data-dismiss="modal">
                    <span aria-hidden="true">&times;</span>
                    <span class="sr-only">Close</span>
                  </button>
                  <h3 class="modal-title" id="myModalLabel1">Edit Account</h3>
                </div>
                <!-- End .modal-header -->
                <div class="modal-body">
                  <div class="form-group">
                    <label for="email2" class="form-label">
                      Your Username
                    </label>
                    <input type="text" class="form-control" placeholder="Username" v-model="user.name" />
                  </div>
                  <!-- End .form-group -->
                  <div class="form-group">
                    <label for="password2" class="form-label">
                      Your email
                    </label>
                    <input type="email" class="form-control" placeholder="email" v-model="user.email" />
                  </div>
                  <!-- End .form-group -->
                  <div class="form-group">
                    <label for="password2" class="form-label">
                      Profile Picture
                    </label>
                    <input type="text" class="form-control" placeholder="profile_pic" v-model="user.profile_pic" />
                  </div>
                  <!-- End .form-group -->
                  <div class="form-group">
                    <label for="password2" class="form-label">
                      Favorite Game
                    </label>
                    <input type="text" class="form-control" placeholder="Game" v-model="user.fav_game" />
                  </div>
                  <!-- End .form-group -->
                  <div class="form-group">
                    <label for="password2" class="form-label">
                      Favorite Movie
                    </label>
                    <input type="text" class="form-control" placeholder="Movie" v-model="user.fav_movie" />
                  </div>
                  <!-- End .form-group -->
                  <div class="form-group">
                    <label for="password2" class="form-label">
                      Favorite Band
                    </label>
                    <input type="text" class="form-control" placeholder="Band" v-model="user.fav_band" />
                  </div>
                  <!-- End .form-group -->
                  <div class="form-group">
                    <label for="password2" class="form-label">
                      Bio
                    </label>
                    <input type="text" class="form-control" placeholder="Bio" v-model="user.bio" />
                  </div>
                  <!-- End .form-group -->
                  <div class="form-group">
                    <label for="password2" class="form-label">
                      Banner
                    </label>
                    <input
                      type="text"
                      name="password2"
                      id="password2"
                      class="form-control"
                      placeholder="Banner Image URL"
                      v-model="user.banner"
                    />
                  </div>
                  <!-- End .form-group -->
                </div>
                <!-- End .modal-body -->
                <div class="modal-footer">
                  <button type="button" class="btn btn-black" data-dismiss="modal">Close</button>
                  <button v-on:click="updateUser()" class="btn btn-custom">Submit</button>
                </div>
                <!-- End .modal-footer -->
              </div>
              <!-- End .modal-content -->
            </div>
            <!-- End .modal-dialog -->
          </form>
        </div>
        <!-- End .modal -->
      </div>
      <!--End .table-cell  -->
    </div>
    <!-- End .table-row -->
    <div class="mb65 mb55-sm"></div>

    <div class="container-fluid text-center">
      <header class="title-block">
        <h2 class="title custom2 text-center">
          My
          <span class="light text-custom">Posts</span>
        </h2>
      </header>
      <ul id="portfolio-filter">
        <li class="active"><a href="#" v-on:click="indexCategory()">All</a></li>
        <li><a href="#" v-on:click="gamesCategory()">Games</a></li>
        <li><a href="#" v-on:click="moviesCategory()">Movies</a></li>
        <li><a href="#" v-on:click="musicCategory()">Music</a></li>
      </ul>
    </div>
    <!-- End .container-fluid -->

    <div class="container-fluid">
      <div class="portfolio-row">
        <div id="portfolio-item-container" class="popup-gallery max-col-4" data-layoutmode="fitRows">
          <div
            v-for="post in filterBy(user.posts, `${category}`, 'category_id')"
            :key="post.id"
            class="portfolio-item web-design wordpress"
          >
            <figure>
              <img v-bind:src="post.image_url" alt="Portfolio Name" />
              <figcaption>
                <a v-bind:href="`/posts/${post.id}`" class="zoom-btn">
                  <i class="fa fa-search"></i>
                </a>
              </figcaption>
            </figure>
            <div class="portfolio-meta">
              <h3 class="portfolio-title">
                <a v-bind:href="`/posts/${post.id}`" title="Portfolio name">{{ post.title }}</a>
              </h3>
              <!-- End .portfolio-tags -->
            </div>
            <!-- End .portfolio-meta -->
          </div>
          <!-- End .portfolio-item -->
        </div>
        <!-- End .portfolio-item-container -->
      </div>
      <!-- End .row -->
    </div>
    <!-- End .container-fluid -->
  </div>
</template>

<style>
img {
  height: 150px;
}
.table-row {
  padding-top: 0em;
}
</style>

<script>
import axios from "axios";
import Vue2Filters from "vue2-filters";

export default {
  mixins: [Vue2Filters.mixin],
  data: function() {
    return {
      user: {},
      owner: "",
      category: "",
    };
  },
  created: function() {
    axios.get("/api/users/" + this.$route.params.id).then(response => {
      console.log("success", response.data);
      this.user = response.data;
    });
    if (this.$route.params.id == this.$parent.getUser()) {
      this.owner = true;
    } else {
      this.owner = false;
    }
  },
  methods: {
    editUser: function() {
      document.querySelector("#edit-user").showModal();
    },
    updateUser: function() {
      var params = {
        name: this.user.name,
        email: this.user.email,
        profile_pic: this.user.profile_pic,
        bio: this.user.bio,
        fav_game: this.user.fav_game,
        fav_movie: this.user.fav_movie,
        fav_band: this.user.fav_band,
        banner: this.user.banner,
      };
      axios.patch("/api/users/" + this.$route.params.id, params).then(response => {
        console.log("success", response.data);
        response.data = this.user;
      });
    },
    gamesCategory: function() {
      // eslint-disable-next-line prettier/prettier
      this.category = "1";
    },
    indexCategory: function() {
      // eslint-disable-next-line prettier/prettier
      this.category = "";
    },
    musicCategory: function() {
      // eslint-disable-next-line prettier/prettier
      this.category = "2";
    },
    moviesCategory: function() {
      // eslint-disable-next-line prettier/prettier
      this.category = "3";
    },
  },
};
</script>
