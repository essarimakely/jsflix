<template>
  <header>
    <router-link to="/">
      <h1><span>Js </span>FLIX</h1>
    </router-link>
  </header>
  <main>
    <router-view />
  </main>
</template>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Fira Sans", sans-serif;
}
body {
  background-color: black;
}
a {
  text-decoration: none;
}
header {
  align-items: center;
  justify-content: center;
  padding: 10px 16px;
  background-color: black;
  box-shadow: 0px, 0px, 6px rgba(0, 0, 0, 0.1);
}
h1 {
  color: white;
  font-size: 36px;
  span {
    color: rgb(235, 235, 15);
  }
}
</style>
