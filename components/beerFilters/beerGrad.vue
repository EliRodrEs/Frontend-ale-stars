<template>
  <div>
    <b-form-select v-model="gradSelected" :options="options" @change="changeGrad" class="mb-3">
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
      gradSelected: null,
      options: [
        { value: "1", text: "<6%" },
        { value: "2", text: "Between 6% and 9%" },
        { value: "3", text: ">9%" }
      ]
    };
  },
  methods: {
    changeGrad() {
      this.$emit("gradSelected", this.gradSelected);
    }
  }
};
</script>
