<template>

  <div>
    <h1>Witaj w systemie do zapisów na zajęcia</h1>

    <div v-if="authenticatedUsername != ''">
        <h3>Jesteś zalogowany jako: {{ authenticatedUsername}}</h3>
        <a @click="logMeOut()">Wyloguj</a>
    </div>

    <div v-else>
      <login-form @login="logMeIn($event)"></login-form>
    </div>
  </div>
</template>

<script>
import "milligram";
import LoginForm from "./LoginForm";


export default {
  components: {LoginForm},
  data() {
  return {
    authenticatedUsername: ''
  };
},
  methods: {
    logMeIn(username) {
      this.authenticatedUsername = username;
    },
    logMeOut() {
      this.authenticatedUsername = '';
    }
  }
}
</script>

<style>
</style>
