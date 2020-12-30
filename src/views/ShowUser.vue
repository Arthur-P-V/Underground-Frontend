<template>
  <div>
    <img v-bind:src="user.profile_pic" v-bind:alt="user.name" />
    <h1>{{ user.username }}</h1>
    <h2>Post Count: {{ user.total_posts }}</h2>
    <h2>Comment Count: {{ user.total_comments }}</h2>
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
        <button v-on:click="updateUser">Update</button>
        <button>close</button>
      </form>
    </dialog>
  </div>
</template>

<style>
img {
  height: 150px;
}
</style>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      user: {},
      owner: "",
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
      };
      axios.patch("/api/users/" + this.$route.params.id, params).then(response => {
        console.log("success", response.data);
        response.data = this.user;
      });
    },
  },
};
</script>
