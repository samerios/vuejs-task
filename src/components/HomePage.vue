<template>
  <v-container fluid class="home-page-container">
    <h3>Change zone selection to get cities by zone</h3>

    <SelectOption
      :items="zones"
      label="Zone"
      value-field="id"
      displayField="name"
      @selection-changed="zonesSelectionChanged"
    ></SelectOption>
    <SelectOption
      :items="copyOfCities"
      label="City"
      valueField="id"
      displayField="name"
    ></SelectOption>
  </v-container>
</template>

<script>
import SelectOption from "./Template/SelectOption.vue";

export default {
  components: { SelectOption },
  name: "HomePage",
  data: () => ({
    // Zones array of objects
    zones: [
      { id: 1, name: "North" },
      { id: 2, name: "South" },
      { id: 3, name: "center" },
    ],

    // Cities array of objects
    cities: [
      { id: 1, name: "Akko", zoneId: 1 },
      { id: 2, name: "Nahariya", zoneId: 1 },
      { id: 3, name: "Tel-aviv", zoneId: 3 },
      { id: 4, name: "Herziliya", zoneId: 3 },
      { id: 5, name: "Beer-sheva", zoneId: 2 },
      { id: 6, name: "Ashdod", zoneId: 2 },
      { id: 7, name: "Haifa", zoneId: 1 },
      { id: 8, name: "Jerusalem", zoneId: 3 },
      { id: 9, name: "Netanya", zoneId: 3 },
      { id: 10, name: "Rehovot", zoneId: 2 },
      { id: 11, name: "Ashkelon", zoneId: 2 },
      { id: 12, name: "Shlomi", zoneId: 1 },
    ],

    // copy of cities In order to keep a copy of the array
    // so as not to lose data after filter
    copyOfCities: [],
  }),
  created() {
    // When component crated copy cities array in copyOfCities
    this.copyOfCities = structuredClone(this.cities).sort(function (a, b) {
      return a.name > b.name ? 1 : b.name > a.name ? -1 : 0;
    });
    this.zonesSelectionChanged(this.zones[0]);
  },
  methods: {
    /**
     * Zone selection changed method, runs when zones select changed to update cities array
     * @param {*} zone selected zone
     */
    zonesSelectionChanged(zone) {
      if (zone) {
        this.copyOfCities = this.cities
          .filter((val) => val.zoneId === zone.id)
          .sort(function (a, b) {
            return a.name > b.name ? 1 : b.name > a.name ? -1 : 0;
          });
        console.log(this.cities);
      }
    },
  },
};
</script>

<style scoped>
/* Home page container class */
.home-page-container {
  height: 100%;
}
</style>
