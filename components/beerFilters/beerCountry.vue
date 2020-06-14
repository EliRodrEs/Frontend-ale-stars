<template>
  <div>
    <b-form-select
      v-model="selected"
      :options="options"
      @Change="changeCountry(value)"
      class="mb-3"
    >
      <!-- This slot appears above the options from 'options' prop -->
      <template v-slot:first>
        <b-form-select-option :value="null">-- Country --</b-form-select-option>
      </template>
    </b-form-select>
  </div>
</template>

<script>
export default {
  props: ["value"],
  data() {
    return {
      selected: null,
      options: [
        { value: "", text: "Select country" },
        { value: "Australia", text: "Australia" },
        { value: "Belgium", text: "Belgium" },
        { value: "Germany", text: "Germany" },
        { value: "Spain", text: "Spain" },
        { value: "Sweden", text: "Sweden" },
        { value: "United States", text: "United States" }
      ]
    };
  },
  methods: {
    changeCountry(value) {
      this.$emit("countrySelected", value);
    }
  }
};
</script>
