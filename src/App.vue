<template>
  <div class="home">
    <h1>LOGIN CON OAUTH</h1>

    <div v-if="!$auth.loading">
      <div v-if="!$auth.isAuthenticated">
        <b-button variant="primary" @click="login"> Iniciar Sesion </b-button>
      </div>
      <div v-if="$auth.isAuthenticated">
        <div class="mt-4">
          <b-card img-alt="Profile picture" img-left class="mb-1" img-top style="max-width: 800px;">
            <b-card-text class="d-flex align-items-center">
              <img :src="$auth.user.picture" alt="Profile picture" style="width: 250px; height: auto; border-radius: 50%; object-fit: cover;" class="mr-4" />
              <div style="margin-left: 30px">
                <b-row>
                  <b-col md="12">
                    <h5 class="mb-3">Nombre:</h5>
                    <strong>{{ $auth.user.given_name }}</strong>
                  </b-col>
                  <b-col md="12">
                    <h5 class="mb-3">Apellidos:</h5>
                    <strong>{{ $auth.user.family_name }}</strong>
                  </b-col>
                  <b-col md="12">
                    <h5 class="mb-3">Email:</h5>
                    <strong>{{ $auth.user.email }}</strong>
                  </b-col>
                </b-row>
              </div>
            </b-card-text>
          </b-card>
        </div>

        <b-button variant="danger" @click="logout"> Cerrar Sesion </b-button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "home",

  methods: {
    login() {
      this.$auth.loginWithRedirect();
    },
    logout() {
      this.$auth.logout({
        logoutParams: {
          returnTo: window.location.origin,
        },
      });
    },
  },
};
</script>
