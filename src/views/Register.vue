<template>
  <h1>Registrar</h1>
  <p><input type="text" placeholder="Correo" v-model="email" /></p>
  <p><input type="password" placeholder="Contraseña" v-model="password" /></p>
  <p><button @click="register">Enviar</button></p>
  <p><button @click="signInWithGoogle">Registrar con Google</button></p>
</template>

<script lang="ts">
import { Vue } from "vue-class-component";
import { getAuth, createUserWithEmailAndPassword } from "firebase/auth";
import { useRouter } from "vue-router";

export default class Register extends Vue {
  email = "";
  password = "";

  router = useRouter();

  register() {
    createUserWithEmailAndPassword(
      getAuth(),
      this.email,
      this.password
    )
      .then((data) => {
        console.log("Usuario registrado!");
        this.router.push("/feed");
      })
      .catch((error) => {
        console.log(error.code);
        alert(error.message);
      });
  }

  signInWithGoogle() {
    console.log("Google!");
  }
}
</script>