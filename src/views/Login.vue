<template>
  <div class="login">
    <form v-on:submit.prevent="submit()">
      <h1>Login</h1>
      <ul>
        <li class="text-danger" v-for="error in errors" :key="error.id">{{ error }}</li>
      </ul>
      <!-- <div class="form-group">
        <label>Email:</label>
        <input type="email" class="form-control" v-model="email" />
      </div> -->
      <div class="input-group input-lg">
        <span class="input-group-addon">Email*</span>
        <input type="email" required="" class="form-control" placeholder="Your Email" v-model="email" />
      </div>
      <!-- <div class="form-group">
        <label>Password:</label>
        <input type="password" class="form-control" v-model="password" />
      </div> -->
      <div class="input-group input-lg">
        <span class="input-group-addon">Password*</span>
        <input type="password" required="" class="form-control" placeholder="Enter Password" v-model="password" />
      </div>
      <input type="submit" class="btn btn-custom signup" value="Submit" />
    </form>
  </div>
</template>

<style>
.login {
  width: 800px;
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
      email: "",
      password: "",
      errors: [],
    };
  },
  methods: {
    submit: function() {
      var params = {
        email: this.email,
        password: this.password,
      };
      axios
        .post("/api/sessions", params)
        .then(response => {
          axios.defaults.headers.common["Authorization"] = "Bearer " + response.data.jwt;
          localStorage.setItem("jwt", response.data.jwt);
          localStorage.setItem("user_id", response.data.user_id);
          this.$router.push("/");
        })
        // eslint-disable-next-line no-unused-vars
        .catch(error => {
          this.errors = ["Invalid email or password."];
          this.email = "";
          this.password = "";
        });
    },
  },
};
</script>
