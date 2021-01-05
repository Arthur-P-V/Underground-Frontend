<template>
  <div>
    <h1>{{ post.title }}</h1>
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
    </div>
  </div>
</template>
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
    }
  },
};
</script>
