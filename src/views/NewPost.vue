<template>
  <div class="home">
    <div class="form-group">
      <label>Title   </label>
      <input type="text" class="form-control" v-model="Title" />
    </div>
    <div class="form-group">
      <label>Content  </label>
      <input type="text" class="form-control" v-model="Content" />
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
      Title: "",
      Content: "",
    };
  },
  created: function() {},
  methods: {
    createPost: function() {
      var params = {
        title: this.Title,
        content: this.Content,
      };
      // eslint-disable-next-line no-unused-vars
      axios.post("/api/posts", params).then(response => {
        this.$router.push("/");
      });
    },
  },
};
</script>
