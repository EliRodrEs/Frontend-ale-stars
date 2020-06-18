<template>
  <div>
    <b-form-select v-model="typeSelected" :options="options" class="mb-3" @change="changeType">
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
      typeSelected: null,
      options: [
        { value: "Ale", text: "Ale" },
        { value: "Lager", text: "Lager" }
      ]
    };
  },
  methods: {
    changeType() {
      this.$emit("typeSelected", this.typeSelected);
    }
  }
};
</script>
