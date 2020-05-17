<template>
  <div id="app">
    <div class="navbar-fixed">
      <nav class="deep-orange darken-1">
        <div class="nav">
          <div class="container">
            <router-link to="/" class="brand-logo">Covid-19 Info</router-link>
            <a href="#" data-target="on-mobile" class="sidenav-trigger">
              <i class="fas fa-bars"></i>
            </a>
            <ul class="right hide-on-med-and-down">
              <li>
                <router-link to="/"> <i class="fas fa-home"></i> Beranda</router-link>
              </li>
              <li>
                <router-link to="/about"><i class="fas fa-info-circle"></i> Tentang Aplikasi</router-link>
              </li>
            </ul>
          </div>
        </div>
      </nav>
    </div>

    <ul class="sidenav" id="on-mobile">
      <li>
        <router-link to="/"> <i class="fas fa-home"></i> Home</router-link>
      </li>
      <li>
        <router-link to="/about"><i class="fas fa-info-circle"></i> About</router-link>
      </li>
    </ul>
    <transition name="fade" mode="out-in">
      <keep-alive>
        <router-view />
      </keep-alive>
    </transition>
  </div>
</template>

<script>
export default {
  mounted() {
    var elems = document.querySelectorAll('.sidenav');
    var instances = M.Sidenav.init(elems);
  },
};
</script>

<style>
  #app {
    font-family: 'Balsamiq Sans', cursive !important;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
  }

  .fade-enter-active, .fade-leave-active {
    transition: opacity .1s;
  }

  .fade-enter, .fade-leave-to {
    opacity: 0;
  }

  .brand-logo {
    font-size: 20px;
  }

</style>
