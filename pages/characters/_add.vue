<template>
  <section class="container">
    <template>
      <div class="container">
        <h1 class="title">
          {{ title }}
        </h1>
        <div class="content">
          <form name="contact" action="http://localhost:3000/characters" method="post" @submit="checkForm">
            <label class="form-label" for="url">
              URL:
            </label>
            <input class="form-field" name="url" id="url" v-model="url"/>
            <label class="form-label" for="name">
              Name:
            </label>
            <input class="form-field" name="name" id="name" v-model="name"/>
            <label class="form-label" for="gender">
              Gender:
            </label>
            <input class="form-field" name="gender" id="gender" v-model="gender"/>
            <input class="form-button" type="submit" />
          </form>
        </div>
      </div>
    </template>
  </section>
</template>
<script>
  import axios from "../../plugins/axios";

  export default{
    data(){
      return{
        title: "Ajouter un personnage de Game of Thrones",
        url : "https://www.anapioficeandfire.com/api/characters/583",
        name : "Arya Stark",
        gender : "Female",
        character : {}
      }
    },
    methods: {
      checkForm: function(e){
        this.character['url'] = this.url;
        this.character['name'] = this.name;
        this.character['gender'] = this.gender;
          axios.post('/characters', this.character)
      }
    }
  }
</script>
