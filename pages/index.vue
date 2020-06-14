<template>
  <div>
    <SecondNav></SecondNav>
    <h1 class="text-center quote" style="font-size:1.5rem;">DA' BEST <span class="or-span">BEERS</span>!!</h1>
    <section id="Top-rated-beers">
      <Beers></Beers>
    </section>
  </div>
</template>

<script>
import Beers from '@/components/Beers.vue'
import SecondNav from '@/components/SecondNav.vue'

export default {
  components: {
    Beers,
    SecondNav
  },
  methods: {

  },

}
</script>

