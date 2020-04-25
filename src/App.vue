<template>

  <div>
    <h1>Witaj w systemie do zapisów na zajęcia</h1>

    <div v-if="authenticatedUsername != ''">
        <h3>Jesteś zalogowany jako: {{ authenticatedUsername}}</h3>
        <a @click="logMeOut()">Wyloguj</a>
    </div>


    <div v-else>
      <!-- <input type="text" v-model="email">
      <button @click="logMeIn()">Zaloguj</button> -->
      <login-form @login="logMeIn($event)"></login-form>
    </div>
    <!-- <h1>Twój email to: {{ email }}</h1> -->
    <!-- <div v-if="email.length < 10">Ale masz krótki adres!</div>
    <div v-else-if="email.length < 15">Twój adres e-mail jest w sam raz.</div>
    <div v-else>Twój adres e-mail jest stanowczo za długi.</div> -->
    <!-- <div>Zaloguj się e-mailem</div> -->
    <!-- <input type="email" v-model="email"> -->
    <!-- <button @click="alertMyEmail()">Wyświetl mój e-mail w alercie</button> -->
    <!-- <button @click="alertMyEmail()">Wchodzę</button> -->


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
