<template>
<div class="bg-image-intro">
    <div class="container">
    <!-- Si el usuario NO está identificado, Le mostramos la opción de loguearse o crear cuenta -->
      <div class="row col-12 align-items-end">
          <h1 class="col big-titles align-self-end"> </h1>
           <div class="w-100"></div><!-- Sin estas dos primeras líneas, no se centra xDDD -->
           <h1 class="col big-titles align-self-end"> </h1>
           <div class="w-100"></div><!-- Sin estas dos segundas líneas, no baja al fondo xDDD -->
          <div class="form col">
            <input type="text" v-model="email" class="col align-self-center" placeholder="User email">
            <button @click="resetPassword" class="btn-main btn col align-self-center">SEND EMAIL</button>
            <a href="/"  class="white-link col align-self-center text-center">Return home</a>
          </div>

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
    }
  },
  methods: {
    async resetPassword(){
      let email = {
        email : this.email
      }
      try {
        let response = await this.$axios.post('auth/resetPassword', email)
        location.href='/emailSent'
      } catch (err) {
        alert(err.message)
      }
    }
  }

}
</script>
