<template>
  <div id='quote-box'>
    <h1>Random Quotes</h1>
    <p id='author'>{{ author }}</p>
    <p id='text'>{{ quote }}</p>
    <button id='new-quote'
      @click='getRandomQuote'>New quote</button>
    <a id='tweet-quote' :href=url>
      Tweet
    </a>
  </div>
</template>

<script>
export default {
  name: 'quote-box',
  props: [ 'author', 'quote' ],
  methods: {
    getRandomQuote() {
      this.$emit('new')
    },
    tweetQuote() {
      this.$emit('tweet')
    }
  },
  computed: {
    url() {
      const quoteString = `${this.quote}%0A${this.author}`
      let url = `https://twitter.com/intent/tweet?text=${quoteString}`
      console.log(url)
      return url
    }
  }
}
</script>

<style>
#quote-box {
  margin: auto;
  width: 75vw;
}

</style>
