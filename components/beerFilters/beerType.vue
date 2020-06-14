<template>
  <div>
    <b-form-select v-model="selected" :options="options" class="mb-3" @Change="changeType(value)">
      <!-- This slot appears above the options from 'options' prop -->
      <template v-slot:first>
        <b-form-select-option :value="null">-- Type --</b-form-select-option>
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
        { value: "", text: "Select type" },
        { value: "Ale", text: "Ale" },
        { value: "Lager", text: "Lager" }
      ]
    };
  },
  methods: {
    changeType(value) {
      this.$emit("styleSelected", value);
    }
  }
};
</script>
