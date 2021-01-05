<template>
  <div id="app">
    <h1>Underground</h1>
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
              <a v-if="isLoggedIn()" v-bind:to="`/users/${this.getUser}`" role="button" aria-expanded="false">
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
              <label>Find Us:</label>
              <a href="#" class="social-icon" title="Facebook"><i class="fa fa-facebook"></i></a>
              <a href="#" class="social-icon" title="Twitter"><i class="fa fa-twitter"></i></a>
              <a href="#" class="social-icon" title="Github"><i class="fa fa-github"></i></a>
              <a href="#" class="social-icon" title="Linkedin"><i class="fa fa-linkedin"></i></a>
              <a href="#" class="social-icon" title="Tumblr"><i class="fa fa-tumblr"></i></a>
              <a href="#" class="social-icon" title="Flickr"><i class="fa fa-flickr"></i></a>
              <a href="#" class="social-icon" title="Snapchat"><i class="fa fa-snapchat"></i></a>
              <a href="#" class="social-icon" title="Vine"><i class="fa fa-vine"></i></a>
            </div>
            <!-- End .social-icons -->
          </div>
          <!-- End .footer-left -->

          <div class="footer-right">
            <ul class="footer-menu">
              <li class="active"><a href="#">Home</a></li>
              <li><a href="#">Services</a></li>
              <li><a href="#">Features</a></li>
              <li><a href="#">FaQS</a></li>
              <li><a href="#">Support</a></li>
              <li><a href="#">Contact Us</a></li>
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
export default {
  methods: {
    getUser: function() {
      return localStorage.getItem("user_id");
    },
    isLoggedIn: function() {
      if (localStorage.getItem("jwt")) {
        return true;
      } else {
        return false;
      }
    },
  },
};
</script>
