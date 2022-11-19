<template>
  <v-col cols="6">
    <v-select
      v-model="select"
      :items="items"
      :item-text="displayField"
      :item-value="valueField"
      :label="label"
      @change="selectionChanged"
      persistent-hint
      return-object
      single-line
    ></v-select>
  </v-col>
</template>

<script>
export default {
  name: "SelectOption",
  props: {
    // Array of items
    items: Array,

    // Label of select
    label: String,

    // Value field usually id
    valueField: String,

    // Display field usually name
    displayField: String,
  },
  data() {
    return {
      // Current select by default is the first
      select: this.items[0],
    };
  },
  methods: {
    /**
     * Selection changed function for event emit
     * @param {*} selected The select object
     */
    selectionChanged(selected) {
      this.$emit("selection-changed", selected);
    },
  },
  watch: {
    /** whenever items changes, this function will run and update 'select' */
    items: function () {
      this.select = this.items[0];
    },
  },
  emits: ["selection-changed"],
};
</script>

<style scoped>
</style>