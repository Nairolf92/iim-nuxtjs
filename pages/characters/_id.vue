<template>
  <div v-if="currentCharacter">
    <h1>{{currentCharacter.name}}</h1>
    <p>{{currentCharacter.id}}</p>
    <p>{{currentCharacter.url}}</p>
    <p>{{currentCharacter.gender}}</p>
    <nuxt-link :to="{name: 'characters'}">
      <button>Retour</button>
    </nuxt-link>
  </div>
</template>
<script>
  import axios from "~/plugins/axios";

  export default{

    async asyncData({ params }){
      const {data} = await axios.get(`/characters/${params.id}`);
      return {
        currentCharacter: data
      }
    },
    data(){
      return{
        currentCharacter: null,
      }
    },

    head() {
      return {
        title: `${this.currentCharacter.name} | Mon site internet` ,
        meta: [
          {}
        ]
      }
    },
  }
</script>
