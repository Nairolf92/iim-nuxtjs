<template>
  <div v-if="currentArticle">
    <h1>{{currentArticle.name}}</h1>
    <p>{{currentArticle.description}}</p>
    <nuxt-link :to="{name: 'blog'}">
      <button>Retour au blog</button>
    </nuxt-link>
  </div>
</template>
<script>
  import axios from "~/plugins/axios";

  export default{

    async asyncData({ params }){
      const {data} = await axios.get(`/servers/${params.id}`);
      console.log(data);
      return {
        currentArticle: data
      }
    },
    data(){
      return{
        currentArticle: null,
      }
    },

    head() {
      return {
        title: "Article",
        meta: [
          {}
        ]
      }
    },
  }
</script>
