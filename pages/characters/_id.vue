<template>
  <section class="container">
        <h1 class="title">
          {{ title }}
        </h1>
        <div class="content" v-if="currentCharacter">
          <form name="contact" action="http://localhost:3000/characters" method="post" @submit="modifyCharacter">
            <label class="form-label" for="url">
              URL:
            </label>
            <input class="form-field" name="url" id="url" v-model="currentCharacter.url"/>
            <label class="form-label" for="name">
              Name:
            </label>
            <input class="form-field" name="name" id="name" v-model="currentCharacter.name"/>
            <label class="form-label" for="gender">
              Gender:
            </label>
            <input class="form-field" name="gender" id="gender" v-model="currentCharacter.gender"/>
            <input class="form-button" type="submit" />
          </form>
          <button v-on:click="deleteCharacter">Supprimer</button>
        </div>
        <nuxt-link :to="{name: 'characters'}">
          <button>Retour</button>
        </nuxt-link>
  </section>
</template>

<script>
  import axios from "~/plugins/axios";

  export default{

    async asyncData({ params }){
      const {data} = await axios.get(`/characters/${params.id}`);
      return {
        loadedCharacter : data,
        currentCharacter : data
      }
    },
    data(){
      return{
        loadedCharacter : null,
        currentCharacter: null,
        title : "Modifier ou supprimer un personnage"
      }
    },
    methods: {
      modifyCharacter: function(e){
        axios.put(`/characters/${this.loadedCharacter.id}`, this.currentCharacter)
      },
      deleteCharacter: function(e){
        axios.delete(`/characters/${this.loadedCharacter.id}`, this.loadedCharacter)

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
