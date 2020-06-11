<template>
  <div>
    <SecondNav></SecondNav>
    <auth></auth>
  </div>
</template>

<script>
import Logo from '~/components/Logo.vue'
import MainNavWeb from '@/components/MainNavWeb.vue'
import auth from '@/components/auth.vue'
import SecondNav from '@/components/SecondNav.vue'

export default {
  components: {
    Logo,
    MainNavWeb,
    auth,
    SecondNav
  }
}
</script>
