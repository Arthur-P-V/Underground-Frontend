<template>
  <div id="app">
    <div class="header-bottom">
      <div class="container-fluid">
        <button
          type="button"
          class="navbar-toggle collapsed"
          data-toggle="collapse"
          data-target="#main-nav-container"
          aria-expanded="false"
        >
          <span class="toggle-text">Menu</span>
          <span class="toggle-wrapper">
            <span class="sr-only">Toggle Menu</span>
            <span class="icon-bar"></span>
            <span class="icon-bar"></span>
            <span class="icon-bar"></span>
          </span>
        </button>
        <div class="collapse navbar-collapse" id="main-nav-container">
          <ul class="nav navbar-nav">
            <li class="dropdown active">
              <a href="/" role="button" aria-expanded="false">
                Home
              </a>
            </li>
            <li>
              <a v-if="!isLoggedIn()" href="/signup" role="button" aria-expanded="false">
                Sign Up
              </a>
            </li>
            <li>
              <a v-if="!isLoggedIn()" href="/login" role="button" aria-expanded="false">
                Log In
              </a>
            </li>
            <li>
              <a v-if="isLoggedIn()" href="/posts/new" role="button" aria-expanded="false">
                Create Post
              </a>
            </li>
            <li>
              <a v-if="isLoggedIn()" v-bind:href="`/users/${this.getUser()}`" role="button" aria-expanded="false">
                Your Account
              </a>
            </li>
            <li>
              <a v-if="isLoggedIn()" href="/logout" role="button" aria-expanded="false">
                Log Out
              </a>
            </li>
          </ul>
        </div>
        <!-- /.navbar-collapse -->
      </div>
      <!-- End .container-fluid -->
    </div>
    <div
      v-if="!isLoggedIn()"
      class="page-header largest parallax custom text-center"
      style="background-image:url(https://images.unsplash.com/photo-1600697230088-4992c83b2804?ixid=MXwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=1050&q=80)"
      data-0="background-position:50% 50%;"
      data-top-bottom="background-position:50% 100%"
    >
      <div class="container-fluid">
        <h1 data-300-top="opacity:1;transform:scale(1);" data-top-bottom="opacity:0.4;transform:scale(1.9);">
          Underground
        </h1>
      </div>
    </div>
    <div
      v-else
      class="page-header largest parallax custom text-center"
      v-bind:style="{ backgroundImage: 'url(' + user.banner + ')' }"
      data-0="background-position:50% 50%;"
      data-top-bottom="background-position:50% 100%"
    >
      <div class="container-fluid">
        <h1 data-300-top="opacity:1;transform:scale(1);" data-top-bottom="opacity:0.4;transform:scale(1.9);">
          Underground
        </h1>
      </div>
    </div>
    <!-- <img
      v-if="!isLoggedIn()"
      src="https://images.unsplash.com/photo-1600697230088-4992c83b2804?ixid=MXwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=1050&q=80"
      alt=""
    />
    <img v-else :src="user.banner" alt="" /> -->
    <!-- End .header-bottom -->
    <!-- <div id="nav">
      <router-link to="/">Home</router-link>
      |
      <router-link to="/about">About</router-link>
      |
      <router-link v-if="!isLoggedIn()" to="/signup">Signup</router-link>
      |
      <router-link v-if="!isLoggedIn()" to="/login">Login</router-link>
      |
      <router-link v-if="isLoggedIn()" to="/logout">Logout</router-link>
      |
      <router-link v-if="isLoggedIn()" to="/posts/new">Create Post</router-link>
      |
      <router-link v-if="isLoggedIn()" :to="`/users/${getUser()}`">Your Account</router-link>
    </div> -->
    <router-view />
    <footer class="footer">
      <div class="footer-bottom">
        <div class="container-fluid">
          <div class="footer-left">
            <div class="social-icons">
              <label>Find Me:</label>
              <a href="https://github.com/Arthur-P-V" class="social-icon" title="Github">
                <i class="fa fa-github"></i>
              </a>
              <a href="https://www.linkedin.com/in/arthurpv/" class="social-icon" title="Linkedin">
                <i class="fa fa-linkedin"></i>
              </a>
            </div>
            <!-- End .social-icons -->
          </div>
          <!-- End .footer-left -->

          <div class="footer-right">
            <ul class="footer-menu">
              <li><a href="/">Home</a></li>
            </ul>
            <p class="copyright">
              <strong>Bold</strong>
              multipurpose template - All rights reserved - 2016 &copy; Made by
              <a href="http://eonythemes.com" target="_blank" title="eonythemes">eonythemes</a>
              .
            </p>
          </div>
          <!-- End .footer-right -->
        </div>
        <!-- End .container-fluid -->
      </div>
      <!-- End .footer-bottom -->
    </footer>
    <!-- End .footer -->
  </div>
</template>

<style></style>

<script>
import axios from "axios";
/* eslint-disable no-unused-vars */
/* eslint-disable no-undef */

export default {
  data: function() {
    return {
      user: {},
    };
  },
  mounted: function() {
    if (this.isLoggedIn()) {
      axios.get("/api/users/" + this.getUser()).then(response => {
        this.user = response.data;
        console.log("success", response.data);
      });
    }
  },
  methods: {
    isLoggedIn: function() {
      if (localStorage.getItem("jwt")) {
        // axios.get("/api/users/" + this.getUser()).then(response => {
        //   this.user = response.data;
        //   console.log("success", response.data);
        // });
        return true;
      } else {
        console.log("not logged in");
        return false;
      }
    },
    getUser: function() {
      return localStorage.getItem("user_id");
    },
  },
};
</script>
