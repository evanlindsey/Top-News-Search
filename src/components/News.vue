<template>
  <div class="news">
    <!--source show/hide button-->
    <button class="btn-source" @click="hidden = !hidden">{{ hidden ? "Show Sources" : "Hide Sources" }}</button>
    <div :class="{'hidden' : hidden }">
      <!--source toggle button-->
      <button class="btn-toggle" @click="toggleAll">Toggle All</button>
      <!--source list-->
      <ul class="sources">
        <!--checkbox for each-->
        <li v-for="(source, index) in sources[0]" :key="source">
          <input type="checkbox" v-model="selected" :value="source">{{ sources[1][index] }}
        </li>
      </ul>
    </div>
    <div>
      <!--search text input-->
      <input class="search-text" type="text" v-model="term" placeholder="Search Term" />
      <!--seach button-->
      <button class="btn-search" @click="term.length > 0 ? search() : null">Search</button>
    </div>
    <!--show results-->
    <div v-if="articles[0].length > 0">
      <h1>Article Results:</h1>
      <!--article list-->
      <ul class="articles">
        <!--link for each-->
        <li v-for="(article, index) in articles[0]" :key="article">
          <a :href="articles[1][index]" target="_blank">{{ article }}</a>
        </li>
      </ul>
    </div>
    <!--no results-->
    <div v-else>
      <h1 v-if="hasSearched">No Results</h1>
    </div>
  </div>
</template>

<script>
// news api urls
const sourceURL = "https://newsapi.org/v1/sources?language=en";
const articleURL = "https://newsapi.org/v1/articles?source=";
const apiKey = "&apiKey=e4320e9e570641a3bc9ef83c44170390";

export default {
  name: 'news',
  // class vars
  data() {
    return {
      sources: [],
      selected: [],
      articles: [[]],
      hidden: true,
      hasSearched: false,
      term: "",
    }
  },
  // onload
  mounted() {
    this.getSources();
  },
  // class methods
  methods: {
    getSources() {
      var results = [];
      // ids
      results[0] = [];
      // names
      results[1] = [];
      // get available sources
      fetch(sourceURL)
        // parse response as json
        .then(response => response.json())
        // handle data
        .then(data => {
          // for each source
          data.sources.forEach((source) => {
            // add id/name to list
            results[0].push(source.id);
            results[1].push(source.name);
          });
        })
        .catch(error => console.log(error));
      // add results to source list
      this.sources = results;
      // seed v-model
      this.selected = this.sources[0];
    },
    toggleAll() {
      // select/deselect all sources
      if (this.selected.length != this.sources[0].length) {
        this.selected = this.sources[0];
      } else {
        this.selected = [];
      }
    },
    search() {
      this.hasSearched = true;
      var results = [];
      // titles
      results[0] = [];
      // urls
      results[1] = [];
      // for each chosen source
      var counter = 0;
      this.selected.forEach((source) => {
        // get top news articles
        fetch(articleURL + source + apiKey)
          // parse response as json
          .then(response => response.json())
          // handle data
          .then(data => {
            // for each article
            data.articles.forEach((article) => {
              var title = article.title;
              var url = article.url;
              // if article title contains search term
              if (title.toLowerCase().includes(this.term.toLowerCase())) {
                // add title/url to list
                results[0].push(title);
                results[1].push(url);
                counter++;
              }
            });
          })
          .catch(error => console.log(error));
      });
      // add results to article list
      this.articles = results;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  margin: 0 auto;
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  padding-left: 0;
}

.sources {
  padding: 0 20px;
  -ms-flex-wrap: wrap;
  flex-wrap: wrap;
}

.sources li {
  text-align: left;
  -webkit-box-flex: 1;
  -ms-flex: 1 300px;
  flex: 1 300px;
}

.articles {
  -webkit-box-orient: vertical;
  -webkit-box-direction: normal;
  -ms-flex-direction: column;
  flex-direction: column;
}

.articles li {
  padding: 5px;
}

button {
  border: none;
  padding: 10px 25px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  margin: 4px 2px;
  cursor: pointer;
  width: 170px;
}

.btn-source {
  background-color: #fff;
  color: #2c3e50;
  border: 2px solid #2c3e50;
  ;
}

.btn-search {
  background-color: #2c3e50;
  color: #fff;
}

.btn-toggle {
  background-color: transparent;
  color: #42b983;
}

.search-text {
  padding: 10px 25px;
  margin-top: 25px;
  width: 250px;
}

.hidden {
  display: none;
}
</style>
