<template>
  <div>
    <SecondNav></SecondNav>
    <userProfileInfo></userProfileInfo>
    <userLists></userLists>
  </div>
</template>

<script>
import SecondNav from '@/components/SecondNav.vue'
import userProfileInfo from '@/components/userProfile/userProfileInfo'
import userLists from '@/components/userProfile/userLists'

export default {
  components: {
    SecondNav,
    userProfileInfo,
    userLists
  }
}
</script>
