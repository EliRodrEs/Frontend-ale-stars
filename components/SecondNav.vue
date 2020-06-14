<template>
  <div>
    <b-navbar toggleable="lg" type="dark"  id="new-nav-bar">
      <b-navbar-brand href="/" class="a-logo"><h1 class="big-titles" id="logo-web"> ALE-  <span><fa icon="beer" class="main-logo-img"/></span>-STARS</h1></b-navbar-brand>
      <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>
      <b-collapse id="nav-collapse" is-nav>
        <!-- Right aligned nav items -->
        <b-navbar-nav class="ml-auto">
          <b-navbar-nav>
            <b-nav-item href="/" >HOME</b-nav-item>
            <b-nav-item href="/beers" >BEERS</b-nav-item>
            <b-nav-item href="/" >CONTACT</b-nav-item>
          </b-navbar-nav>
            <b-nav-item-dropdown right v-if="!isAuth">
            <!-- Using 'button-content' slot -->
            <template v-slot:button-content>
              <em class="white-link">USER</em>
            </template>
            <b-dropdown-item href="/login">LOG IN</b-dropdown-item>
            <b-dropdown-item href="/login#">REGISTER</b-dropdown-item>
            </b-nav-item-dropdown>
            <b-nav-item-dropdown right v-else>
            <!-- Using 'button-content' slot -->
              <template v-slot:button-content>
                <em class="white-link">USER</em>
              </template>
                <b-dropdown-item href="/userProfile">PROFILE</b-dropdown-item>
                <b-dropdown-item @click="logout">LOG OUT</b-dropdown-item>
            </b-nav-item-dropdown>
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>
  </div>
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
      window.localStorage.clear()
      this.checkAuth()
    }
  }
}
</script>
