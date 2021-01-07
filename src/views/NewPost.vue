<template>
  <div class="home">
    <div class="post-form">
      <!-- <select v-model="selected">
        <option disabled value="">Category</option>
        <option value="1">Game</option>
        <option value="2">Music</option>
        <option value="3">Movie</option>
      </select> -->
      <select class="form-control" v-model="selected">
        <option value="1">Game</option>
        <option value="2">Music</option>
        <option value="3">Movie</option>
      </select>
      <!-- <div class="form-group">
        <label>Title   </label>
        <input type="text" class="form-control" v-model="Title" />
      </div> -->
      <div class="input-group">
        <span class="input-group-addon">Title*</span>
        <input v-model="Title" type="text" required="" class="form-control" placeholder="Post Title" />
      </div>
      <!-- <div class="form-group">
        <label>Content</label>
        <input type="text" class="form-control" v-model="Content" />
      </div> -->
      <div class="input-group textarea-container">
        <span class="input-group-addon">Post Body</span>
        <textarea v-model="Content" class="form-control" cols="30" rows="6" placeholder="Post Body"></textarea>
      </div>
      <!-- <div class="form-group">
        <label>Image Url</label>
        <input type="text" class="form-control" v-model="imageUrl" />
      </div> -->
      <div class="input-group input-group-sm">
        <span class="input-group-addon">Image Url*</span>
        <input v-model="imageUrl" type="text" required="" class="form-control" placeholder="Desired Image" />
      </div>
      <button class="btn btn-custom" v-on:click="createPost">Create</button>
    </div>
  </div>
</template>

<style>
.post-form {
  width: 900px;
  display: block;
  margin-left: auto;
  margin-right: auto;
  padding-bottom: 1em;
}
</style>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      selected: "",
      Title: "",
      Content: "",
      imageUrl: "",
    };
  },
  created: function() {},
  methods: {
    createPost: function() {
      var params = {
        title: this.Title,
        content: this.Content,
        image_url: this.imageUrl,
        category_id: this.selected,
      };
      // eslint-disable-next-line no-unused-vars
      axios.post("/api/posts", params).then(response => {
        this.$router.push("/");
      });
    },
  },
};
</script>
