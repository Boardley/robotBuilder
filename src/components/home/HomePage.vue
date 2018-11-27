<template>
  <div class="hello">
    <div>
      <img class="img-robot" src="../../assets/robot-home.png" alt="Build-A-Bot" aria-hidden="true">
    </div>
    <div class="get-started">
      <router-link to="/build">Get started</router-link> building your first robot!
    </div>
    <!-- /.get-started -->
  </div>
</template>

<script>
export default {
  name: 'HomePage',
  props: {
    msg: String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss">
.hello {

  a {
    color: #42b983;
  }
  h3 {
    margin: 40px 0 0;
  }
  ul {
    list-style-type: none;
    padding: 0;
  }
  li {
    display: inline-block;
    margin: 0 10px;
  }

  .img-robot {
    display: block;
    margin: 0 auto;
    max-width: 40%;
  }

  .get-started {
    font-size: 28px;
    font-weight: bold;
    text-align: center;
  }
}

</style>
