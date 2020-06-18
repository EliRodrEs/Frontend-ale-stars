<template>
  <div>
    <b-form-select v-model="styleSelected" :options="options" class="mb-3" @change="changeStyle">
      <!-- This slot appears above the options from 'options' prop -->
      <template v-slot:first>
        <b-form-select-option :value="null">-- Style --</b-form-select-option>
      </template>
    </b-form-select>

    <!--     <div class="mt-3">Selected: <strong>{{ selected }}</strong></div> -->
  </div>
</template>

<script>
export default {
  props: ["value"],
  data() {
    return {
      styleSelected: null,
      options: [
        { value: "Brown Ale", text: "Brown Ale" },
        { value: "IPA", text: "IPA" },
        { value: "Pilsner", text: "Pilsner" },
        { value: "Stout", text: "Stout" }
      ]
    };
  },
  methods: {
    changeStyle() {
      this.$emit("styleSelected", this.styleSelected);
    }
  }
};
</script>
