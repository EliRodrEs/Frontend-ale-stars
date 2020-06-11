<template>
<div class="bg-image-intro">
    <div class="container">
    <!-- Si el usuario NO está identificado, Le mostramos la opción de loguearse o crear cuenta -->
      <div v-if="!isAuth" class="row col-12 justify-content-center">
          <h1 class="col big-titles align-self-start">  </h1>
           <div class="w-100"></div>
          <div v-if="showLogin" class="form col">
            <input type="text" v-model="email" class="col align-self-center" placeholder="User email">
            <input type="password" v-model="password" class="col align-self-center" placeholder="Password">
            <button @click="login" class="btn-main btn col align-self-center">LOG IN</button>
            <a href="#" @click="showLogin=false" class="white-link col align-self-center">New here? Create an account!</a>
            <a href="/pageResetPassword" class="white-link col align-self-center">Forgot your password?</a>
          </div>
          <div v-else class="form col">
            <input type="text" v-model="name" placeholder="Name" class="col align-self-center">
            <input type="text" v-model="surname" placeholder="Surname" class="col align-self-center">
            <input type="email" v-model="email" placeholder="Email" class="col align-self-center">
            <input type="password" v-model="password" placeholder="Password" class="col align-self-center">
            <button @click="createUser" class="btn-main btn col align-self-center">Crear</button>
            <a href="/login"  class="white-link col align-self-center">Do you have an account?</a>

          </div>
      </div>

    <!-- Si el usuario está identificado, le mostramos un logout -->
      <div v-else class="row">
          <button @click="logout" class="btn-main btn col align-self-center">Log out</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data(){
    return {
      isAuth: false,
      email: "",
      password: "",
      orders: [],
      showLogin: true,
      name: "",
      surname: ""
    }
  },
  mounted() {
    this.checkAuth();
  },
  methods: {
    checkAuth(){
      this.isAuth = window.localStorage.getItem("token")!= null
    },
    async createUser(){
      let newUser = {
        email: this.email,
        password: this.password,
        name: this.name,
        surname: this.surname,
      }

      try{
        let userCreated = await this.$axios.post('users', newUser)

        this.email = ""
        this.name = ""
        this.password = ""
        this.surname = ""
      }catch(err){
        alert(err.message)
      }
    },
    async logout(){
      window.localStorage.removeItem("token")
      this.checkAuth()
    },
    async login(){
      let loginData = {
        email: this.email,
        password: this.password
      }
      try{
        let response = await this.$axios.post("auth", loginData)
        window.localStorage.setItem("token",response.data.token)

        this.checkAuth()
        location.href='/'
      }catch(e){
        console.log("Se ha producido un error")
      }
    }
  },
}
</script>
