<template>
  <div class="page-wrapper">
    <div class="article-cards-wrapper">
      <article-card-block
        v-for="(article, i) in articles"
        :key="article.id"
        :article="article"
        class="article-card-block"
      />
    </div>
  </div>
</template>

<script>
import ArticlecardBlock from '@/components/blocks/ArticleCardBlock'

export default {
  components: {
    ArticleCardBlock
  },
  data () {
    return {
      currentPage: 1,
      articles: []
    }
  },
  async fetch() {
    const articles = await fetch(
      'https://dev.to/api/articles?tag=nuxt&state=rising&page=${this.currentPage}'
    ).then(res => res.json())

    this.articles = this.articles.concat(articles)
  }
}
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family:
    'Quicksand',
    'Source Sans Pro',
    -apple-system,
    BlinkMacSystemFont,
    'Segoe UI',
    Roboto,
    'Helvetica Neue',
    Arial,
    sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
