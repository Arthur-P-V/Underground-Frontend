<template>
  <div class="home">
    <select v-model="selected">
      <option disabled value="">Category</option>
      <option value="1">Game</option>
      <option value="2">Music</option>
      <option value="3">Movie</option>
    </select>
    <div class="form-group">
      <label>Title   </label>
      <input type="text" class="form-control" v-model="Title" />
    </div>
    <div class="form-group">
      <label>Content  </label>
      <input type="text" class="form-control" v-model="Content" />
    </div>
    <div class="form-group">
      <label>Image Url  </label>
      <input type="text" class="form-control" v-model="imageUrl" />
    </div>
    <button v-on:click="createPost">Create</button>
  </div>
</template>

<style></style>

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
