<template>
  <div id="app">
    <nav class="navbar navbar-expand-lg navbar-dark fixed-top" id="mainNav">
      <div class="container">
          <a class="navbar-brand js-scroll-trigger" href="#page-top">FLIXX</a>
          <button class="navbar-toggler navbar-toggler-right" type="button" data-toggle="collapse" data-target="#navbarResponsive" aria-controls="navbarResponsive" aria-expanded="false" aria-label="Toggle navigation">
              Menu
              <i class="fas fa-bars ml-1"></i>
          </button>
          <div class="collapse navbar-collapse" id="navbarResponsive">
              <ul class="navbar-nav text-uppercase ml-auto">
                  <li class="nav-item">
                  <router-link class="nav-link js-scroll-trigger" to="/">Home</router-link>
                  </li>
                  <li class="nav-item">
                  <router-link class="nav-link js-scroll-trigger" to="/movies">Movies</router-link>
                  </li>
                  <li class="nav-item">
                  <router-link class="nav-link js-scroll-trigger" to="/movies/new">Create Movie</router-link>
                  </li>
                  <li class="nav-item">
                  <router-link class="nav-link js-scroll-trigger" to="/about">About</router-link>
                  </li>
                  <li v-if="!isLoggedIn()" class="nav-item">
                  <router-link class="nav-link js-scroll-trigger" to="/signup">Signup</router-link>
                  </li>
                  <li v-if="!isLoggedIn()" class="nav-item">
                  <router-link class="nav-link js-scroll-trigger" to="/login">Login</router-link>
                  </li>
                  <li v-if="isLoggedIn()" class="nav-item">
                  <router-link class="nav-link js-scroll-trigger" to="/logout">Logout</router-link>
                  </li>
              </ul>
          </div>
      </div>
    </nav>
    <!-- Masthead-->
    <header class="masthead">
        <div class="container">
            <div class="masthead-subheading">Let's watch movies!</div>
            <div class="masthead-heading text-uppercase">FLIXX</div>
            <a class="btn btn-primary btn-xl text-uppercase js-scroll-trigger" href="#services">Movie time</a>
        </div>
    </header>
    <router-view/>
  </div>
</template>

<script>
export default {
  data: function() {
    return {};
  },
  created: function() {},
  methods: {
    isLoggedIn: function() {
      return localStorage.getItem("jwt");
    }
  }
};
</script>