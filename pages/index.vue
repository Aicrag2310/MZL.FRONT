<template>
  <div class="login-page">
    <div class="background-container">
      <v-container fluid>
        <v-row align="center" justify="center">
          <v-col cols="12" md="8" lg="6">
            <v-card class="elevation-12 custom-rounded-card center-card">
                <img
                src="../assets/images/logo.png"
                alt="Logo"
                max-height="100"
                width="200px"
                contain
              />
              
              <v-toolbar-title class="v-toolbar-title-global">
                Login
              </v-toolbar-title>
              <v-card-text>
                <v-form @submit.prevent="authUser">
                  <v-text-field
                    outlined
                    v-model="username"
                    label="Username"
                    color="secondary"
                    name="login"
                    prepend-icon="mdi-account"
                    type="text"
                  />
                  <v-text-field
                    outlined
                    v-model="password"
                    id="password"
                    label="Password"
                    color="secondary"
                    name="password"
                    prepend-icon="mdi-lock"
                    type="password"
                    @keypress.enter="authUser"
                  />
                  <v-checkbox
                    v-model="rememberPassword"
                    label="Recordar contraseña"
                    style="margin-bottom: -10%; margin-top: -5%"
                  ></v-checkbox>
                </v-form>
              </v-card-text>
              <v-card-actions>
                <v-btn
                  @click="authUser"
                  class="text-none text-subtitle-1"
                  color="#EF6B48"
                  style="
                    border-radius: 10px;
                    color: white;
                    width: 150px;
                    margin-top: 1%;
                  "
                  >Entrar</v-btn
                >
              </v-card-actions>
              <v-card-actions>
                <v-spacer />
                <v-btn text color="secondary" style="margin-right: 10%"
                  >¿Olvidaste la contraseña?</v-btn
                >
                <!-- Enlace "¿Olvidaste la contraseña?" -->
              </v-card-actions>
              <!-- LOGIN BUTTONS -->
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </div>
  </div>
</template>

<script>
import Swal from "sweetalert2";
export default {
  data() {
    return {
      username: "",
      password: "",
      rememberPassword: false, // Variable para la casilla de verificación
    };
  },
  async asyncData({ error }) {
    if (process.client) {
        console.log("Es cliente ");
    }
    else if (process.server){
        console.log("Es ssr ");
    }

    return {};
  },
  methods: {
    authUser() {
      if (!this.username || !this.password) {
        Swal.fire({
          icon: "error",
          title: "Error",
          text: "Por favor, ingresa un nombre de usuario y una contraseña.",
        });
        return;
      }
      if (this.username == "alex"){
        Swal.fire({
          icon: "success",
          title: "success",
          text: "Bienvenido",
        });
        this.$router.push('/about');
      }
      else{
        Swal.fire({
          icon: "error",
          title: "error",
          text: "Usuario/Contraseña incorrecto.",
        });
      }
    },
  },
};
</script>

<style scoped>
.login-page {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100vh;
}

.background-container {
  background-image: url("../assets/images/background.png");
  background-size: cover;
  background-position: center;
  min-height: 100%;
  min-width: 100%;
}
.custom-rounded-card {
  border-radius: 20px;
  max-width: 400px;
}

.center-card {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100%;
  top: 100px;
  left: 450px;
}

/* Estilos responsivos */
@media (max-width: 600px) {
  .custom-rounded-card {
    max-width: 90%;
  }
  .center-card {
    top: 50px;
    left: 0;
  }
}
</style>
