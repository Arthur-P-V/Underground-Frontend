<template>
  <div>
    <!-- <h1>{{ post.title }}</h1>
    <h3>{{ post.category }}</h3>
    <router-link :to="`/users/${post.user.id}`">
      <h3>{{ post.user.name }}</h3>
    </router-link>
    <img v-bind:src="post.image_url" v-bind:alt="post.title" />
    <p>{{ post.score }}</p>
    <p>{{ post.content }}</p>
    <button v-on:click="destroyModal">Delete</button>
    <dialog id="destroy-post">
      <form method="dialog">
        <h3>Are you sure?</h3>
        <button v-on:click="destroyPost">Delete</button>
        <button>Close</button>
      </form>
    </dialog>
    <div>
      <button v-if="liked == false" v-on:click="postLike()">Like</button>
      <button v-else v-on:click="postUnlike()">Unlike</button>
    </div>
    <button v-on:click="showEdit">Edit</button>
    <dialog id="edit-post">
      <form method="dialog">
        <h3>Title:</h3>
        <input type="text" v-model="post.title" />
        <h3>Content:</h3>
        <input type="text" v-model="post.content" />
        <h3>Image Url:</h3>
        <input type="text" v-model="post.image_url" />
        <button v-on:click="editPost">Submit</button>
        <button>close</button>
      </form>
    </dialog>
    <router-link to="/">Back</router-link>
    <div>
      <textarea name="Comment" cols="40" rows="8" v-model="newComment"></textarea>
      <button v-on:click="createComment">Post</button>
    </div>
    <div v-for="comment in comments" :key="comment.id">
      <h5>{{ comment.user }}</h5>
      <p>{{ comment.comment }}</p>
      <button v-if="user.admin" v-on:click="destroyComment(comment)">Delete</button>
    </div> -->
    <div class="main">
      <div class="container-fluid">
        <article class="entry">
          <div class="entry-media">
            <figure>
              <img v-bind:src="post.image_url" alt="entry image" />
            </figure>
          </div>
          <!-- End .enty-media -->

          <div class="entry-content-container">
            <!-- End .entry-meta -->

            <div class="entry-content-wrapper">
              <h2 class="entry-title">
                {{ post.title }}
              </h2>
              <div class="entry-content">
                <p>{{ post.content }}</p>
              </div>
              <!-- End .entry-content -->
            </div>
            <!-- End .entry-content-wrapper -->
          </div>
          <!-- End .entry-content-container -->
          <div class="author-container">
            <div class="entry-author">
              <figure>
                <img v-bind:src="post.user.profile_pic" alt="Author" class="img-circle" />
              </figure>
              <div class="author-content">
                <h4>
                  <a href="#">{{ post.user.name }}</a>
                </h4>
                <p>
                  {{ post.user.bio }}
                </p>
                <!-- End .social-icons -->
              </div>
              <!-- end .author-content -->
            </div>
            <!-- End .entry-author -->
          </div>
        </article>

        <div class="comments">
          <h3 class="title custom mb25">Comments</h3>
          <ul class="comments-list media-list">
            <li class="media" v-for="comment in comments" :key="comment.id">
              <div class="comment">
                <div class="media-left">
                  <img class="media-object img-circle" v-bind:src="comment.user.profile_pic" alt="User name" />
                </div>
                <!-- End .media-left -->
                <div class="media-body">
                  <h4 class="media-heading">
                    {{ comment.user.name }}
                  </h4>

                  <p>
                    {{ comment.comment }}
                  </p>
                </div>
                <!-- End .media-body -->
              </div>
              <!-- End .comment -->
            </li>
          </ul>
        </div>
        <!-- End .comments -->

        <div id="respond" class="comment-respond">
          <h3 class="title custom mb25">Send a Reply</h3>
          <form action="#" method="post">
            <!-- End .row -->
            <textarea
              class="form-control"
              rows="6"
              placeholder="Add Your Comment"
              v-model="newComment"
              required
            ></textarea>
            <a class="btn btn-custom" v-on:click="createComment">Comment</a>
          </form>
        </div>
        <!-- End #respond -->
      </div>
      <!-- End .container-fluid -->
    </div>
  </div>
</template>

<style>
.author-container {
  padding: 1em;
}
.entry-author {
  padding: 0.5em;
  background-color: white;
  box-shadow: 0 2px 3px rgba(0, 0, 0, 0.1);
}
</style>

<script>
import axios from "axios";
export default {
  data: function() {
    return {
      post: {},
      user: {},
      liked: "",
      vote_id: "",
      comments: [],
      newComment: "",
      owner: "",
    };
  },
  created: function() {
    axios.get("/api/posts/" + this.$route.params.id).then(response => {
      console.log("success", response.data);
      this.post = response.data;
      this.vote_id = response.data.vote_id;
      this.liked = response.data.liked;
    });
    axios.get("/api/comments/" + this.$route.params.id).then(response => {
      console.log("success", response.data);
      this.comments = response.data;
    });
    axios.get("/api/users/" + this.$parent.getUser()).then(response => {
      console.log("success", response.data);
      this.user = response.data;
    });
  },
  // mounted: function() {
  //   if (this.user.id == this.$parent.getUser) {
  //     this.owner = true;
  //     console.log("owner");
  //   } else {
  //     this.owner = false;
  //     console.log("not owner");
  //   }
  // },
  methods: {
    postLike: function() {
      var params = {
        post_id: this.post.id,
        value: 1,
      };
      axios.post("/api/votes", params).then(response => {
        console.log("success", response.data);
        this.vote_id = response.data.id;
        this.liked = true;
        this.post.score += 1;
      });
    },
    postUnlike: function() {
      axios.delete("/api/votes/" + this.vote_id).then(response => {
        console.log("vote destroyed", response.data);
        this.vote_id = false;
        this.liked = false;
        this.post.score -= 1;
      });
    },
    createComment: function() {
      var params = {
        post_id: this.$route.params.id,
        content: this.newComment,
      };
      axios.post("/api/comments", params).then(response => {
        console.log("Success", response.data);
        this.comments.push(response.data);
      });
    },
    destroyPost: function() {
      axios.delete("/api/posts/" + this.$route.params.id).then(response => {
        console.log("success", response.data);
        this.$router.push("/");
      });
    },
    destroyComment: function(comment) {
      axios.delete("/api/comments/" + comment.id).then(response => {
        var index = this.comments.indexOf(comment);
        console.log("success", response.data);
        this.comments.splice(index, 1);
      });
    },
    showEdit: function() {
      document.querySelector("#edit-post").showModal();
    },
    editPost: function() {
      var params = {
        title: this.post.title,
        content: this.post.content,
        image_url: this.post.image_url,
      };
      axios.patch("/api/posts/" + this.$route.params.id, params).then(response => {
        console.log("success", response.data);
      });
    },
    destroyModal: function() {
      document.querySelector("#destroy-post").showModal();
    },
  },
};
</script>
