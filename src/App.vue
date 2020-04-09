<template>
  <div id="app">
    <nav>
      <ul>
        <li class="nav-item">
          <img class="logo" src="./assets/build-a-bot-logo.png">
          Build-a-Bot
        </li>
      </ul>
    </nav>
    <router-view/>
  </div>
</template>

<style lang="less">
body {
    background: linear-gradient(to bottom, #555, #999);
    background-attachment: fixed;
}
</style>


<style scoped lang="less">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
}
main {
  margin: 0;
  padding: 30px;
  background-color: white;
  width: 1024px;
  min-height: 300px;
}
header {
  background-color: #999;
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
  border-right: 1px solid #bbb;
}
.logo {
  vertical-align: middle;
  height: 30px;
}
#nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
