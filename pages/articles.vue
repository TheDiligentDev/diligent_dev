<template>
  <div class="container">
    <b-row class="pt-4" v-if="articles.length > 0">
      <b-col lg="4" md="4" sm="12" v-for="article in articles" :key="article.created">
        <div class="pt-2 pb-2">
          <b-card class="shadow white rounded">
            <h4 class="pb-1 article-title">{{article.title}}</h4>
            <p>{{article.pubDate}}</p>
            <div v-html="article.content"></div>
          </b-card>
        </div>
      </b-col>
    </b-row>
  </div>
</template>

<script>
let Parser = require('rss-parser')
let parser = new Parser()

export default {
  data() {
    return {
      articles: []
    }
  },
  async asyncData({ params }) {
    let feed = await parser.parseURL('https://medium.com/feed/@diligentdev')
    return {
      articles: feed.items
    }
  }
}
</script>

<style>
.medium-feed-image img {
  width: 300px;
  height: 150px;
  object-fit: cover;
  margin: 0;
  padding: 0;
  width: 100%;
  -webkit-box-shadow: 5px 5px 11px -1px rgba(0, 0, 0, 0.75);
  -moz-box-shadow: 5px 5px 11px -1px rgba(0, 0, 0, 0.75);
  box-shadow: 5px 5px 11px -1px rgba(0, 0, 0, 0.75);
  border-radius: 2.5px;
}
.medium-feed-link {
    text-align: center;
}

.medium-feed-link a {
  display: inline-block;
  margin-bottom: 0;
  font-weight: 400;
  text-align: center;
  white-space: nowrap;
  vertical-align: middle;
  touch-action: manipulation;
  cursor: pointer;
  background-image: none;
  border: 1px solid transparent;
  padding: 6px 12px;
  font-size: 14px;
  line-height: 1.42857143;
  border-radius: 4px;
  user-select: none;
  color: #fff;
  background-color: #d9534f;
  border-color: #d43f3a;
  text-align: center;
}

.article-title {
  color: #dc3545;
  overflow: hidden;
  text-overflow: ellipsis;
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-line-clamp: 2; /* number of lines to show */
}

a:hover, a:visited, a:link, a:active
{
    text-decoration: none;
}
</style>