<template>
  <div id="app">
    <header>
      <nav>
        <ul>
          <li class="nav-item">
            <router-link
              exact-active-class="link-active"
              active-class="none"
              :to="{name: 'Home'}"
            >
              <img
                class="logo"
                src="./assets/build-a-bot-logo.png"
                alt="Build-A-Bot"
                aria-hidden="true"
              >
              Build-A-Bot
            </router-link>
          </li>
          <!-- /.nav-item -->
          <li class="nav-item">
            <router-link
              exact-active-class="link-active"
              active-class="none"
              :to="{name: 'Build'}"
            >
              Build
            </router-link>
          </li>
          <!-- /.nav-item -->
          <li class="nav-item">
            <router-link
              active-class="link-active"
              :to="{name: 'BrowseParts'}"
            >
              Browse
            </router-link>
          </li>
          <!-- /.nav-item -->
          <li class="nav-item cart">
            <router-link
              active-class="link-active"
              :to="{name: 'Cart'}"
            >
              Cart
            </router-link>
            <div class="cart-items">
              {{ cart.length }}
            </div>
            <!-- /.cart-items -->
          </li>
          <!-- /.nav-item -->
        </ul>
      </nav>
    </header>
    <div class="container">
      <aside class="aside">
        <router-view name="sidebar" />
      </aside>
      <!-- /.aside -->
      <main>
        <router-view />
      </main>
    </div>
    <!-- /.container -->
  </div>
</template>

<script>
export default {
  name: 'app',
  computed: {
    cart() {
      return this.$store.state.robots.cart;
    }
  },
  methods: {
    toggle: function () {
      this.showRight = !this.showRight;
    },
    toggleAside: function () {
      this.showAside = !this.showAside;
    }
  }
}
</script>

<style lang="scss">
body {
  background: linear-gradient(to bottom, #555, #999);
  background-attachment: fixed;
  font-family: Arial, Helvetica, sans-serif;
}

a {
  color: inherit;
  text-decoration: none;
}
.container {
  display: flex;
  justify-content: center;
  margin: 10px auto;
}

.aside {
  background-color: #aaa;
  min-height: 300px;
  padding: 30px;
  width: 100px;
}

main {
  background-color: #fff;
  min-height: 300px;
  padding: 30px;
  width: 964px;
}

header {
  background-color: #999;
  width: 1184px;
  margin: 0 auto;
}
ul {
  padding: 3px;
  display: flex;
}
.nav-item {
  border-right: 1px solid #bbb;
  display: inline-block;
  font-size: 22px;
  padding: 5px 10px;

  &.cart {
    border-right: none;
    margin-left: auto;
    position: relative;
  }
}
.logo {
  vertical-align: middle;
  height: 30px;
  margin-right: 5px;
}
.link-active {
  color: #fff;
}

.cart-items {
  background-color: mediumseagreen;
  border-radius: 100px;
  font-size: 18px;
  padding: 5px 10px;
  position: absolute;
  right: -20px;
  text-align: center;
  top: -10px;
}

</style>

