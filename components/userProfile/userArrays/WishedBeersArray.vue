<template>
  <Beers v-bind:beers="beers"></Beers>
</template>

<script>
import Beers from '@/components/Beers.vue'
export default {
  data(){
    return {
      beers: []
    }
  },
  async mounted(){
    const userID = localStorage.getItem('id')
    const response = await this.$axios.get(`users/${userID}/wish`)
    this.beers = response.data
  },
  components: {
    Beers
  }
}
</script>
