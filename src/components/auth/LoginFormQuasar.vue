<template>
  <div class="q-pa-md flex flex-center" style="min-height: 100vh">
    <q-card class="q-pa-lg" style="width: 350px; max-width: 90vw;">
      <q-card-section class="bg-primary text-white text-center q-pa-md" style="border-radius: 8px 8px 0 0;">
        <div class="text-h5">Login Form</div>
      </q-card-section>
      <q-form @submit.prevent="iniciarSesion">
        <q-card-section>
          <q-input filled v-model="email" label="Email" type="email" lazy-rules
            :rules="[val => !!val || 'Ingrese su email']" class="q-mb-md" prepend-inner-icon="email"
            autocomplete="username" />
          <q-input filled v-model="password" label="Password" type="password" lazy-rules
            :rules="[val => !!val || 'Ingrese su contraseña']" class="q-mb-md" prepend-inner-icon="lock"
            autocomplete="current-password" />
          <div class="q-mb-md text-right">
            <q-btn flat label="¿Olvidó su contraseña?" size="sm" color="primary" class="q-pa-none"
              @click="onForgotPassword" />
          </div>
          <q-btn type="submit" color="primary" label="Login" class="full-width" :loading="loading" />
        </q-card-section>
        <q-card-actions align="center">
          <span>¿No tienes cuenta?</span>
          <q-btn flat label="Regístrate" color="primary" @click="goToRegister" />
        </q-card-actions>
      </q-form>
    </q-card>
  </div>
</template>

<script>
export default {
  name: 'LoginFormQuasar',
  data() {
    return {
      email: '',
      password: '',
      loading: false
    }
  },
  methods: {
    iniciarSesion() {
      this.loading = true;
      let endpointURL = '/api/User/SignIn';
      let user = {
        email: this.email,
        password: this.password
      };
      this.$api.post(endpointURL, user)
        .then(response => {
          localStorage.setItem('userData', JSON.stringify(response.data));
          this.$q.notify({
            message: 'Bienvenido',
            color: 'positive',
            icon: 'check_circle'
          });
          this.$router.push('/dashboard/product');
        })
        .catch(() => {
          this.$q.notify({
            message: 'Error de autenticación',
            color: 'negative',
            icon: 'error'
          });
        })
        .finally(() => {
          this.loading = false;
        });
    },
    goToRegister() {
      this.$router.push('/register');
    },
    onForgotPassword() {
      this.$q.notify({
        message: 'Funcionalidad no implementada',
        color: 'info',
        icon: 'info'
      });
    }
  }
}
</script>

<style scoped>
.full-width {
  width: 100%;
}
</style>
