<template>
  <div class="wrapper">
    <header class="header">
      <div class="navbar">
        <div class="container">
          <div class="navbar-content">
            <div class="logo">Github Finder</div>
          </div>
        </div>
      </div>
    </header>
    <router-view></router-view>
    <footer class="footer"></footer>
  </div>
</template>

<script>
export default {
  data() {
    return {
      links: []
    }
  }
};
</script>

<style lang="scss">


.navbar-link {
  &.router-link-exact-active  {
      color: rgb(52, 52, 200);
  }
}


</style>
