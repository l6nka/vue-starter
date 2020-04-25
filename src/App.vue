<template>
  <div>
    <h1>Witaj w systemie do zapisów na zajęcia</h1>
    <div v-if="!isLoggedIn">
      <span>Zaloguj się na zajęcia: </span>
      <label>
        <input type="email" v-model="email">
      </label>
      <button @click="logIn()">Wchodzę</button>
    </div>
    <div v-else>
      <div>Witaj {{ email }}</div>
      <div>
        <a href="?" @click="logIn()">Wyloguj</a>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      email: '',
      isLoggedIn: false
    };
  },
  methods: {
    logIn() {
      if (this.email !== ''){
        this.isLoggedIn = !this.isLoggedIn
      }
    }
  }
}
</script>

<style>
</style>
