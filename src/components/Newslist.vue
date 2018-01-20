<template>
  <div class="news-list">
    <div class="container">
      <ul class="media-list">
        <li class="media" v-for="article in articles">
          <div class="media-left">
            <a v-bind:href="article.url" target="_blank">
              <img v-bind:src="article.urlToImage" class="media-object">
            </a>
          </div>
          <div class="media-body">
            <h4 class="media-heading">
              <a v-bind:href="article.url" target="_blank">{{ article.title }}</a>
            </h4>
            <h5><i>by {{ article.author }}</i></h5>
            <p>{{ article.description }}</p>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: 'NewsList',
  props: ['source'],
  data () {
    return {
      articles: []
    }
  },
  methods: {
    updateSouerce (source) {
      this.$http.get('https://newsapi.org/v1/articles?source=' + source + '&apiKey=f14f3cd2235742d89deda799df5d5a80')
        .then(response => {
          this.articles = response.data.articles
        })
    }
  },
  created () {
    this.updateSouerce(this.source)
  },
  watch: {
    source (val) {
      this.updateSouerce(val)
    }
  }
}
</script>

<style scoped>
  .media-object {
    width: 128px;
    padding: 10px;
  }
  .media {
    border-top: 1px solid grey;
    padding-top: 20px;
  }
</style>
