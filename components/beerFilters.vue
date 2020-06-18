<template>
  <div id="filter-group" class="container">
    <ul class="list row">
      <li class="col-6">
        <beerCountry :value="country" @countrySelected="handleCountryChange"></beerCountry>
      </li>
      <li class="col-6">
        <beerGrad :value="grad" @gradSelected="handleGradChange"></beerGrad>
      </li>
      <li class="col-6">
        <beerStyle :value="style" @styleSelected="handleStyleChange"></beerStyle>
      </li>
      <li class="col-6">
        <beerType :value="type" @typeSelected="handleTypeChange"></beerType>
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
      }
    },
  components: {
    beerCountry,
    beerGrad,
    beerStyle,
    beerType
  },
  methods: {
    buildQuery() {
      const query = {
        country: this.country,
        grad: this.grad,
        style: this.style,
        type: this.type
      };

      this.$emit("filterChanged", query);
    },
    handleCountryChange(countrySelected) {
      this.country = countrySelected
      this.buildQuery();
    },
    handleGradChange(gradSelected) {
      this.grad = gradSelected;
      this.buildQuery();
    },
    handleStyleChange(styleSelected) {
      this.style = styleSelected
      this.buildQuery();
    },
    handleTypeChange(typeSelected) {
      this.type = typeSelected
      this.buildQuery();
    }
  }
};
</script>
