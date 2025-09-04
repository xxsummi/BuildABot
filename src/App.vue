<template>
  <header>
    <nav>
      <ul>
        <li class="nav-item">
          <router-link class="nav-link" :to="{ name: 'Home' }" exact>
            <img class="logo" src="./assets/build-a-bot-logo.png" />
            Build a bot
          </router-link>
        </li>
        <li class="nav-item">
          <router-link class="nav-link" :to="{ name: 'Build' }" exact>
            Build
          </router-link>
        </li>
      </ul>
    </nav>
  </header>
  <main>
    <router-view/>
    <!-- <RobotBuilder /> -->
     <!-- <Search/> -->
  </main>
</template>

<script>
// import HomePage from './home/HomePage.vue';
import RobotBuilder from "./build/RobotBuilder.vue";
// import Search from './search/Search.vue';

export default {
  name: "App",
  // components: {
  //   RobotBuilder,
  //   // Search,
  // },
};
</script>

<style>
body {
  background: linear-gradient(to bottom, #fb275f, #ff94ad);
  background-attachment: fixed;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
}
</style>

<style scoped>
main {
  margin: 0 auto;
  padding: 30px;
  background-color: #ffd2dc;
  width: 1024px;
  min-height: 300px;
}
header {
  background-color: #ffd2dc;
  width: 1084px;
  margin: 0 auto;
}
ul {
  padding: 3px;
  display: flex;
}
.nav-item {
  display: inline-block;
  padding: 5px 10px;
  font-size: 22px;
  border-right: 1px solid #ff94ad;
}
.logo {
  vertical-align: middle;
  height: 30px;
}
.nav-link {
  text-decoration: none;
  color: #ff618b;
  /* color: inherit; */
}
/* .nav-link:hover {
  color: #fb275f;
} */
.router-link-active {
  font-weight: bold;
  color: #ff1352;
}
</style>
