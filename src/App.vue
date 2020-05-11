<template>

  <div>
    <h1>System do zapisów na zajęcia</h1>

    <div v-if="authenticatedUsername != ''">
        <h3>Witaj {{ authenticatedUsername}} !</h3>        
        <button style="float: right;" @click="logMeOut()">Wyloguj</button>
        <meeting-page></meeting-page>
    </div>

    <div v-else-if="authenticatedUsername == null">
      <login-form @login="logMeIn($event)"></login-form>
    </div>

    <div v-else>
      <login-form @login="logMeIn($event)"></login-form>
    </div>
  </div>
</template>

<script>
import "milligram";
import LoginForm from "./LoginForm";
import MeetingPage from "./meetings/MeetingPage";

export default {
  components: {LoginForm, MeetingPage},
  data() {
  return {
    authenticatedUsername: JSON.parse(localStorage.getItem('authenticatedUsername'))
  };
},
  methods: {
    logMeIn(username) {
      this.authenticatedUsername = username;
      localStorage.setItem('authenticatedUsername', JSON.stringify(this.authenticatedUsername));

    },
    logMeOut() {
      this.authenticatedUsername = '';        
       localStorage.setItem('authenticatedUsername', JSON.stringify(this.authenticatedUsername));
       localStorage.setItem('loginUser', JSON.stringify(this.authenticatedUsername));
    }
  }
}
</script>

<style>
</style>
