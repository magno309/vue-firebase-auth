<template>
  <nav>
    <router-link to="/">Home</router-link> |
    <router-link to="/feed">Feed</router-link> |
    <router-link to="/register">Registrar</router-link> |
    <router-link to="/sign-in">Login</router-link>
    <button @click="handleLogOut" v-if="isLoggedIn">Cerrar sesión</button>
  </nav>
  <router-view />
</template>

<script lang="ts">
import { Vue } from "vue-class-component";
import { getAuth, onAuthStateChanged, signOut } from "firebase/auth";
import router from "./router";

export default class App extends Vue {

  isLoggedIn = false;
  auth = getAuth();

  mounted() {
    onAuthStateChanged(this.auth, (user) => {
      if(user) {
        this.isLoggedIn = true;
      }else{
        this.isLoggedIn = false;
      }
    });
  }

  handleLogOut = () => {
    signOut(this.auth).then(() => {
      router.push("/");
    })
  };
}
</script>


<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
}
</style>
