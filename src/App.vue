<template>
  <div id="app">
      <Header />
      <router-view />
      <Footer />
  </div>
</template>

<script>
import Header from './components/layout/Header';
import Footer from './components/layout/Footer';

export default {
  name: 'App',
  components: {
    Header,
    Footer
  },
  data() {
    return {

    }
  }
}
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

#app {
  width: 100%;
  height: auto;
  line-height: 1.4;
}
</style>
