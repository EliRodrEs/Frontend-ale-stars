<template>
  <div class="container">
    <div class="row">
      <input type="text" v-model="name" placeholder="Name" class="col align-self-center global-input">
      <input type="text" v-model="surname" placeholder="Surname" class="col align-self-center global-input">
      <input type="email" v-model="email" placeholder="Email" class="col align-self-center global-input">
      <input type="password" v-model="password" placeholder="Password" class="col align-self-center global-input">
      <button @click="createUser" class="btn-main btn col align-self-center">Crear</button>
      <a href="/login"  class="white-link col align-self-center">Do you have an account?</a>
    </div>
  </div>
</template>

<script>
import Swal from "sweetalert2";

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
        Swal.fire({
          position: 'center',
          icon: 'success',
          title: 'Your account has been saved',
          showConfirmButton: false,
        })
        this.email = ""
        this.name = ""
        this.password = ""
        this.surname = ""
        location.href = "/login"
      }catch(err){
        alert(err.message)
      }
    },
    async logout(){
      window.localStorage.removeItem("token")
      this.checkAuth()
    }
  }
}
</script>
