<template>
  <div class="wrapper">
    <h2>Registration</h2>
    <form action="#" autocomplete="off">
      <div class="input-box">
        <input type="text" v-model="user.firstName" placeholder="Enter your first name" required>
      </div>
      <div class="input-box">
        <input type="text" v-model="user.lastName" placeholder="Enter your last name" required>
      </div>
      <div class="input-box">
        <input type="date" v-model="user.dateOfBirth" placeholder="Enter your birthday" required>
      </div>
      <div class="input-box">
        <input type="text" v-model="user.country" placeholder="Enter your country" required>
      </div>
      <div class="input-box">
        <input type="text" v-model="user.address" placeholder="Enter your address" required>
      </div>
      <div class="input-box">
        <input type="text" v-model="user.email" placeholder="Enter your email" required>
      </div>
      <div class="input-box">
        <input type="password" v-model="createPassword" placeholder="Create password" required>
      </div>
      <div class="input-box">
        <input type="password" v-model="user.password" placeholder="Confirm password" required>
      </div>
      <div class="input-box button">
        <input type="button" value="Register Now" @click="registrarUsuario">
      </div>
      <div class="text">
        <h3>Already have an account? <a href="#">Login now</a></h3>
      </div>
    </form>
  </div>

</template>

<style>
@import url('https://fonts.googleapis.com/css?family=Poppins:400,500,600,700&display=swap');

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Poppins', sans-serif;
}

body {
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  background: #4070f4;
}

.wrapper {
  position: relative;
  max-width: 430px;
  width: 100%;
  background: #fff;
  padding: 34px;
  border-radius: 6px;
  box-shadow: 0 5px 10px rgba(0, 0, 0, 0.2);
}

.wrapper h2 {
  position: relative;
  font-size: 22px;
  font-weight: 600;
  color: #333;
}

.wrapper h2::before {
  content: '';
  position: absolute;
  left: 0;
  bottom: 0;
  height: 3px;
  width: 28px;
  border-radius: 12px;
  background: #4070f4;
}

.wrapper form {
  margin-top: 30px;
}

.wrapper form .input-box {
  height: 52px;
  margin: 18px 0;
}

form .input-box input {
  height: 100%;
  width: 100%;
  outline: none;
  padding: 0 15px;
  font-size: 17px;
  font-weight: 400;
  color: #333;
  border: 1.5px solid #C7BEBE;
  border-bottom-width: 2.5px;
  border-radius: 6px;
  transition: all 0.3s ease;
}

.input-box input:focus,
.input-box input:valid {
  border-color: #4070f4;
}

form .policy {
  display: flex;
  align-items: center;
}

form h3 {
  color: #707070;
  font-size: 14px;
  font-weight: 500;
  margin-left: 10px;
}

.input-box.button input {
  color: #fff;
  letter-spacing: 1px;
  border: none;
  background: #4070f4;
  cursor: pointer;
}

.input-box.button input:hover {
  background: #0e4bf1;
}

form .text h3 {
  color: #333;
  width: 100%;
  text-align: center;
}

form .text h3 a {
  color: #4070f4;
  text-decoration: none;
}

form .text h3 a:hover {
  text-decoration: underline;
}
</style>
<script>
export default {
  name: "RegisterForm",
  data() {
    return {
      createPassword: "",
      user: {
        firstName: "",
        lastName: "",
        country: "",
        address: "",
        dateOfBirth: "",
        email: "",
        password: ""
      }
    }
  },
  methods: {
    registrarUsuario() {
      let endpointURL = "/api/User/SignUp";
      //Validate createPassword and user.password
      if (this.createPassword !== this.user.password) {
        this.$q.notify({
          message: "La contraseña no coincide",
          color: "negative",
          icon: "warning",
          timeout: 5000,
          position: "top"
        })
        return;
      }

      this.$api.post(endpointURL, this.user)
        .then(response => {
          this.$q.notify({
            message: "Usuario creado con éxito",
            color: "positive",
            icon: "check_circle",
            timeout: 5000,
            position: "top"
          })
          this.$router.push("/");
        }).catch(error => {
          this.$q.notify({
            message: "Error al crear el usuario",
            color: "negative",
            icon: "error",
            timeout: 5000,
            position: "top"
          })
        })

    }
  }
}
</script>
