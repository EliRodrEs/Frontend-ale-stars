<template>
  <div>
    <b-form-select v-model="selected" :options="options" class="mb-3" @Change="changeStyle(value)">
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
      selected: null,
      options: [
        { value: "", text: "Select Style" },
        { value: "Brown Ale", text: "Brown Ale" },
        { value: "IPA", text: "IPA" },
        { value: "Pilsner", text: "Pilsner" },
        { value: "Stout", text: "Stout" }
      ]
    };
  },
  methods: {
    changeStyle(value) {
      this.$emit("styleSelected", value);
    }
  }
};
</script>
