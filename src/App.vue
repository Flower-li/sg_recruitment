<template>
  <div id="app">
    <router-view />
  </div>
</template>

<style lang="scss">
html {
  height: 100%;
}
body {
  margin: 0;
  height: 100%;
}
#app {
  margin: 0;
  padding: 0;
  font-family: "Microsoft YaHei", sans-serif;
  height: 100%;
  font-size: 14px;
}
h1,
h2,
h3,
h4,
h4,
h5,
p,
ul {
  margin-block-start: 0em;
  margin-block-end: 0em;
  margin-inline-start: 0px;
  margin-inline-end: 0px;
  padding-inline-start: 0px;
}
li {
  list-style-type: none;
}
a {
  text-decoration: none;
}
</style>
