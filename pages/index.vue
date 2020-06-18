<template>
  <div>
    <SecondNav></SecondNav>
    <section id="loading-img" v-if="!isLoaded">
      <Animation></Animation>
    </section>
    <section id="Top-rated-beers" v-else>
      <h1 class="text-center quote" style="font-size:1.5rem;">DA' BEST <span class="or-span">BEERS</span>!!</h1>
      <Beers v-bind:beers="beers"></Beers>
    </section>
  </div>
</template>

<script>
import Beers from '@/components/Beers.vue'
import SecondNav from '@/components/SecondNav.vue'
import Animation from '@/components/Animation.vue'

export default {
  data(){
    return {
      isLoaded: false,
      beers: []
    }
  },
  async mounted() {
    let response = await this.$axios.get("/beers");
    this.beers = response.data;
    this.isLoaded = true
  },
  components: {
    Beers,
    SecondNav,
    Animation
  },
  }


</script>

