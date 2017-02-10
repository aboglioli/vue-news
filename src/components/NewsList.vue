<template>
  <div class="news-list">
    <div class="container">
      <ul class="media-list">
        <li class="media" v-for="article in articles">
          <div class="media-left">
            <a v-bind:href="article.url" target="_blank">
              <img class="media-object" v-bind:alt="article.description" v-bind:src="article.urlToImage" />
            </a>
          </div>
          <div class="media-body">
            <h4 class="media-heading">
              <a v-bind:href="article.url" target="_blank">{{article.title}}</a>
            </h4>
            <h5><i>{{article.author}}</i></h5>
            <p>
              {{article.description}}
            </p>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: 'news-list',
  props: ['source', 'apiKey'],
  data() {
    return {
      articles: []
    };
  },
  methods: {
    updateSource(source) {
      this.$http
        .get(`https://newsapi.org/v1/articles?source=${source.id}&apiKey=${this.apiKey}`)
        .then(res => {
          this.articles = res.data.articles;
        });
    }
  },
  watch: {
    source(val) {
      this.updateSource(val)
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
    border-top: 1px solid lightgrey;
    padding-top: 20px;
  }
</style>
