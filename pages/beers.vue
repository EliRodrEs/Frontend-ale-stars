<template>
  <div>
    <SecondNav></SecondNav>
    <div>
      <h1 class="text-center" id="quote">"<span class="or-span">Beauty</span> is in the eyes of the <span class="or-span">Beerholder</span>"</h1>
    </div>
      <Beers></Beers>
  </div>
</template>

<script>
import Beers from '@/components/Beers.vue'
import SecondNav from '@/components/SecondNav.vue'

export default {
  components: {
    Beers,
    SecondNav
  }
}
</script>
