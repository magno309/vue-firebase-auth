<template>
  <h1>Login</h1>
  <p><input type="text" placeholder="Correo" v-model="email" /></p>
  <p><input type="password" placeholder="Contraseña" v-model="password" /></p>
  <p v-if="errorMsg">{{ errorMsg }}</p>
  <p><button @click="register">Enviar</button></p>
  <p><button @click="signInWithGoogle">Entrar con Google</button></p>
</template>

<script lang="ts">
import { Vue } from "vue-class-component";
import { getAuth, signInWithEmailAndPassword } from "firebase/auth";
import { useRouter } from "vue-router";

export default class SignIn extends Vue {
  email = "";
  password = "";
  errorMsg = "";

  router = useRouter();

  register() {
    signInWithEmailAndPassword(getAuth(), this.email, this.password)
      .then((data) => {
        console.log("Usuario Logeado!");
        this.router.push("/feed");
      })
      .catch((error) => {
        console.log(error.code);
        switch (error.code) {
          case "auth/invalid-email":
            this.errorMsg = "Correo invalido!";
            break;
          case "auth/user-not-found":
            this.errorMsg = "No existe una cuenta con ese correo!";
            break;
          case "auth/wrong-password":
            this.errorMsg = "Contraseña incorrecta!";
            break;
          default:
            this.errorMsg = "Correo o contraseña incorrectos!";
            break;
        }
      });
  }

  signInWithGoogle() {
    console.log("Google!");
  }
}
</script>