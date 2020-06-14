<template>
  <div id="filter-group" class="container">
    <ul class="list row">
      <li class="col-6">
        <beerCountry :value="country"></beerCountry>
      </li>
      <li class="col-6">
        <beerGrad :value="grad"></beerGrad>
      </li>
      <li class="col-6">
        <beerStyle :value="style"></beerStyle>
      </li>
      <li class="col-6">
        <beerType :value="type"></beerType>
      </li>
    </ul>
  </div>
</template>


<script>
import beerCountry from "@/components/beerFilters/beerCountry";
import beerGrad from "@/components/beerFilters/beerGrad";
import beerStyle from "@/components/beerFilters/beerStyle";
import beerType from "@/components/beerFilters/beerType";

export default {
  data() {
    return {
      country: "",
      grad: "",
      style: "",
      type: ""
    };
  },
  components: {
    beerCountry,
    beerGrad,
    beerStyle,
    beerType
  },
  methods: {
    buildQuery() {
      const query = {};
      if (this.country !== "") {
        query.country = this.country;
      }
      if (this.grad !== "") {
        query.grad = this.grad;
      }
      if (this.style !== "") {
        query.style = this.style;
      }
      if (this.type !== "") {
        query.type = this.type;
      }
      return query;
    },
    async executeQuery() {
      const response = await this.$axios.get("beers", { params: buildQuery() });
    }
  }
};
</script>
