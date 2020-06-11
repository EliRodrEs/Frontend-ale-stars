<template>
	<nav class="navBar">

      <a class="a-logo" href="/"><h1 class="big-titles" id="logo-web"> <span><fa icon="beer" class="main-logo-img"/></span>ALE-STARS</h1></a>
    <ul class="list">
        <li><a href="/" class="white-link">Home</a></li>
        <li><a href="/" class="white-link">Beers</a></li>
        <li><a href="/" class="white-link">Browser</a></li>
        <li><a href="/" class="white-link">Contact</a></li>
        <li v-if="!isAuth"><a href="/login" class="white-link">Log in/Sign in</a></li>
        <li v-else><a href="#" @click="logout">Log out</a></li>
    </ul>
  </nav>
</template>

<script>

import { fas } from '@fortawesome/free-solid-svg-icons'

export default {
computed: {
      fas () {
        return fas
      },
    },
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
    async logout(){
      window.localStorage.removeItem("token")
      this.checkAuth()
    }
  }
}
</script>
