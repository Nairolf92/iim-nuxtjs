<template>
  <section class="container">
    <h2>{{title}}</h2>
    <ul>
      <li v-for="article in articles" :key="article.id">
        <nuxt-link :to="{name: 'blog-id', params: {id: article.id}}">
          {{ article.name }}
        </nuxt-link>
      </li>
    </ul>
  </section>
</template>
<script>
  import axios from "../../plugins/axios";

  export default{
    async asyncData(){
      const {data} = await axios.get('/servers');
      console.log(data);
      return {
        articles : data
      }
    },
    data(){
      return{
        currentArticles: null,
        title: "Mes articles",
        articles: [
        ]
      }
    },
    mounted(){

      this.currentArticles = this.articles.find(item => item.id === this.$route.params.id);
    }
  }
</script>
