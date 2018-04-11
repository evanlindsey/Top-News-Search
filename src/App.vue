<template>
  <div id="app">
    <a href="https://github.com/evanlindsey/Top-News-Search"><img style="position: absolute; top: 0; right: 0; border: 0;" src="https://camo.githubusercontent.com/e7bbb0521b397edbd5fe43e7f760759336b5e05f/68747470733a2f2f73332e616d617a6f6e6177732e636f6d2f6769746875622f726962626f6e732f666f726b6d655f72696768745f677265656e5f3030373230302e706e67" alt="Fork me on GitHub" data-canonical-src="https://s3.amazonaws.com/github/ribbons/forkme_right_green_007200.png"></a>
    <h1>TOP NEWS SEARCH</h1>
    <news></news>
    <footer>&#169 2018 Evan Lindsey<br />Powered by:
      <a href="https://newsapi.org/" target="_blank">News API</a>
    </footer>
  </div>
</template>

<script>
import News from './components/News'

export default {
  name: 'app',
  components: {
    News
  }
}
</script>

<style>
body {
  background: #ffffff url("./assets/news.jpg") no-repeat center center fixed;
  background-size: cover;
}

h1 {
  padding-top: 5px;
  text-shadow: 0 1px 0 #ccc,
  0 2px 0 #c9c9c9,
  0 3px 0 #bbb,
  0 4px 0 #b9b9b9,
  0 5px 0 #aaa,
  0 6px 1px rgba(0, 0, 0, .1),
  0 0 5px rgba(0, 0, 0, .1),
  0 1px 3px rgba(0, 0, 0, .3),
  0 3px 5px rgba(0, 0, 0, .2),
  0 5px 10px rgba(0, 0, 0, .25),
  0 10px 10px rgba(0, 0, 0, .2),
  0 20px 20px rgba(0, 0, 0, .15);
}

a {
  color: #42b983;
}

footer {
  margin-top: 30px;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background-color: #ffffff;
  margin: 60px 10px;
  padding-bottom: 20px;
  border: 5px solid #2c3e50;
}
</style>
