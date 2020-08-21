<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <Quotes
      :author='author' 
      :quote='quote'
      @new='getRandomQuote'
      @tweet='tweetQuote'
    />
  </div>
</template>

<script>
import Quotes from './components/Quotes.vue'

export default {
  name: 'App',
  components: {
    Quotes
  },
  data: () => ({
    quote: '-',
    author: '-',
    quotes: []
  }),
  methods: {
    getQuotes() {
      return new Promise((fulfill, reject) => {
      const quoteUrl = 'https://gist.githubusercontent.com/camperbot/5a022b72e96c4c9585c32bf6a75f62d9/raw/e3c6895ce42069f0ee7e991229064f167fe8ccdc/quotes.json'

      fetch(quoteUrl)
        .then(response => response.json())
        .then(data => fulfill(data))
          .catch(error => reject(error))
      })
    },
    getRandomQuote() {
      const i = Math.floor(Math.random() * Math.floor(this.quotes.length))
      console.log(i)
      const obj = this.quotes[i]
      this.quote = obj.quote
      this.author = obj.author
    },
    tweetQuote() {
      return
    }
  },
  beforeMount() {
    this.getQuotes().then(data => {
      this.quotes = data.quotes
      this.getRandomQuote()
    })
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
img {
  width: 200px;
}
</style>
