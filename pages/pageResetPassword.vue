<template>
  <div>
    <SecondNav></SecondNav>
    <reset-password> </reset-password>
  </div>
</template>

<script>
import Logo from '~/components/Logo.vue'
import resetPassword from '@/components/resetPassword.vue'
import MainNavWeb from '@/components/MainNavWeb.vue'
import SecondNav from '@/components/SecondNav.vue'

export default {
  components: {
    Logo,
    resetPassword,
    MainNavWeb,
    SecondNav
  }
}
</script>
