<template>
  <section class="container">
    <h2>{{title}}</h2>
    <ul>
      <li v-for="character in characters" :key="character.id">
        <nuxt-link :to="{name: 'characters-id', params: {id: character.id}}">
          {{ character.name }}
        </nuxt-link>
      </li>
    </ul>
  </section>
</template>
<script>
  import axios from "../../plugins/axios";

  export default{
    async asyncData(){
      const {data} = await axios.get('/characters');
      return {
        characters : data
      }
    },
    data(){
      return{
        currentCharacters: null,
        title: "Personnages de Game of Thrones",
        characters: [
        ]
      }
    },
    mounted(){

      this.currentCharacters = this.characters.find(item => item.id === this.$route.params.id);
    }
  }
</script>
