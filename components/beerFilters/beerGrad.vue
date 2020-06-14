<template>
  <div>
    <b-form-select v-model="selected" :options="options" @Change="changeGrad(value)" class="mb-3">
      <!-- This slot appears above the options from 'options' prop -->
      <template v-slot:first>
        <b-form-select-option :value="null">-- ABV --</b-form-select-option>
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
        { value: "", text: "Select grad" },
        { value: "x < 6", text: "<6%" },
        { value: "6<= x < 9", text: "Between 6% and 9%" },
        { value: "9<= x", text: ">9%" }
      ]
    };
  },
  methods: {
    changeGrad(value) {
      this.$emit("gradSelected", value);
    }
  }
};
</script>
