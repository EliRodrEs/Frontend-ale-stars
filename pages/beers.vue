<template>
  <div>
    <SecondNav></SecondNav>
    <section id="loading-img" v-if="!isLoaded">
      <Animation></Animation>
    </section>
    <div v-else>
      <div>
        <h1 class="text-center quote">
        " <span class="or-span">Beauty</span> is in the eyes of the <span class="or-span">Beerholder</span>"
        </h1>
      </div>
      <beerFilters @filterChanged="handleFilterChange"></beerFilters>
      <Beers v-bind:beers="beers"></Beers>
    </div>
  </div>
</template>

<script>
import Beers from "@/components/Beers.vue";
import SecondNav from "@/components/SecondNav.vue";
import beerFilters from "@/components/beerFilters.vue";
import Animation from  '@/components/Animation.vue';

export default {
  data() {
    return {
      isLoaded: false,
      beers: [],
      query: {
        country: "",
        grad: "",
        style: "",
        type: ""
      }
    };
  },
  mounted() {
    this.getFilteredBeers();
  },
  components: {
    Beers,
    SecondNav,
    beerFilters,
    Animation
  },
  methods: {
    async getFilteredBeers() {
      try {
        let response = await this.$axios.get("beers", { params: this.query });
        this.beers = response.data
        this.isLoaded = true
      } catch (error) {}
    },
    handleFilterChange(query) {
      this.query = query
      this.getFilteredBeers()
    }
  }
};
</script>
