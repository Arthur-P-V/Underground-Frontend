<template>
  <div class="signup">
    <form v-on:submit.prevent="submit()">
      <h1>Signup</h1>
      <ul>
        <li class="text-danger" v-for="error in errors" :key="error.id">{{ error }}</li>
      </ul>
      <!-- <div class="form-group">
        <label>Name:</label>
        <input type="text" class="form-control" v-model="name" />
      </div> -->
      <div class="input-group">
        <span class="input-group-addon">Username*</span>
        <input type="text" required="" class="form-control" placeholder="Your Username" v-model="name" />
      </div>
      <!-- End .input-group -->
      <!-- <div class="form-group">
        <label>Email:</label>
        <input type="email" class="form-control" v-model="email" />
      </div> -->
      <div class="input-group">
        <span class="input-group-addon">Email*</span>
        <input type="email" required="" class="form-control" placeholder="Your Email" v-model="email" />
      </div>
      <!-- End .input-group -->
      <!-- <div class="form-group">
        <label>Password:</label>
        <input type="password" class="form-control" v-model="password" />
      </div> -->
      <div class="input-group">
        <span class="input-group-addon">Password*</span>
        <input type="password" required="" class="form-control" placeholder="Enter Password" v-model="password" />
      </div>
      <!-- End .input-group -->
      <!-- <div class="form-group">
        <label>Password confirmation:</label>
        <input type="password" class="form-control" v-model="passwordConfirmation" />
      </div> -->
      <div class="input-group">
        <span class="input-group-addon">Password Confirm*</span>
        <input
          type="password"
          required=""
          class="form-control"
          placeholder="Confirm Password"
          v-model="passwordConfirmation"
        />
      </div>
      <!-- End .input-group -->
      <input type="submit" class="btn btn-custom signup" value="Submit" />
    </form>
  </div>
</template>

<style>
.signup {
  width: 800px;
  display: block;
  margin-left: auto;
  margin-right: auto;
  padding-bottom: 1em;
}
.btn.btn-custom.signup {
  display: block;
  margin-left: auto;
  margin-right: auto;
}
</style>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      name: "",
      email: "",
      password: "",
      passwordConfirmation: "",
      errors: [],
    };
  },
  methods: {
    submit: function() {
      var params = {
        name: this.name,
        email: this.email,
        password: this.password,
        password_confirmation: this.passwordConfirmation,
      };
      axios
        .post("/api/users", params)
        // eslint-disable-next-line no-unused-vars
        .then(response => {
          this.$router.push("/login");
        })
        .catch(error => {
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>
