<template>
  <div>
    <SecondNav></SecondNav>
    <div>
      <h1 class="text-center quote">"<span class="or-span">Beauty</span> is in the eyes of the <span class="or-span">Beerholder</span>"</h1>
    </div>
      <beerFilters></beerFilters>
      <Beers></Beers>
  </div>
</template>

<script>
import Beers from '@/components/Beers.vue'
import SecondNav from '@/components/SecondNav.vue'
import beerFilters from '@/components/beerFilters.vue'


export default {
  components: {
    Beers,
    SecondNav,
    beerFilters
  }
}
</script>
