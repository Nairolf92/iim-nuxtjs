<template>
  <div v-if="currentArticle">
    <h1>{{currentArticle.title}}</h1>
    <p>{{currentArticle.content}}</p>
    <nuxt-link :to="{name: 'blog'}">
      <button>Retour au blog</button>
    </nuxt-link>
  </div>
</template>
<script>
  export default{

    data(){
      return{
        currentArticle: null,
        articles: [
          {id: 1, title: 'Articles1', content: '...'},
          {id: 2, title: 'Articles2', content: '...'},
          {id: 3, title: 'Articles3', content: '...'},
          {id: 4, title: 'Articles4', content: '...'},
        ]
      }
    },

    head() {
      return {
        title: "Article",
        meta: [

        ]
      }
    },

    mounted(){
      this.currentArticle = this.articles.find(item => item.id === this.$route.params.id);
    }
  }
</script>
