<template>
<div class="bg-image-intro">
    <div class="">
    <!-- Si el usuario NO está identificado, Le mostramos la opción de loguearse o crear cuenta -->
      <div v-if="!isAuth" class="">
          <div v-if="showLogin" class="form-inline">
            <input type="text" v-model="email" class="input-inline" placeholder="User email">
            <input type="password" v-model="password" class="input-inline" placeholder="Password">
            <a href="#" @click="login" class="white-link">LOG IN</a>
          </div>
      </div>

    <!-- Si el usuario está identificado, le mostramos un logout -->
      <div v-else class="row">
          <a href="#" @click="logout" class="white-link col align-self-center">Log out</a>
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
/*     resetpassword(){
      let auth = firebase.auth()
      let email = this.email

      auth.sendPasswordResetEmail(email).then(function (){
        //email sent
      }). catch(err) {
        //An error happened
      }
    }, */
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
      }catch(e){
        console.log("Se ha producido un error")
      }
    }
  },
}
</script>
