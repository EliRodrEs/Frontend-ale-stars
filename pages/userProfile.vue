<template>
  <div>
    <SecondNav></SecondNav>
<!--     <section id="loading-img" v-if="!isLoaded">
      <Animation></Animation>
    </section> -->
    <div> <!-- V-ELSE DEBERÍA IR AQUÍ -->
      <userProfileInfo></userProfileInfo>
      <userLists></userLists>
    </div>
  </div>
</template>

<script>
import SecondNav from '@/components/SecondNav.vue'
import userProfileInfo from '@/components/userProfile/userProfileInfo'
import userLists from '@/components/userProfile/userLists'
import Animation from '@/components/Animation.vue'

export default {
  components: {
    SecondNav,
    userProfileInfo,
    userLists,
    Animation
  }
}
</script>
