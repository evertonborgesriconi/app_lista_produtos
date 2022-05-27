<template>
  <div id="app">
    <header>
      <HeaderTop />
    </header>
    <main>
      <ListaProdutos />
    </main>
    <footer>
      <FooterEnd />
    </footer>
  </div>
</template>

<script>
import HeaderTop from "./components/HeaderTop.vue";
import ListaProdutos from "./components/ListaProdutos.vue";
import FooterEnd from "./components/FooterEnd.vue";

export default {
  name: "App",
  components: {
    HeaderTop,
    ListaProdutos,
    FooterEnd,
  },
};
</script>

<style>
* {
  box-sizing: border-box;
  padding: 0;
  margin: 0;
}
body {
  background-color: whitesmoke;
}
#app {
  display: flex;
  min-height: 100vh;
  flex-direction: column;
}
main {
  flex: 1;
}
</style>
