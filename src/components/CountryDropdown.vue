<template>
  <DropdownComponent
    v-model="value"
    :items="items"
    placeholder="Select country"
  />
</template>

<script>
import { reactive } from "vue";
import DropdownComponent from "./DropdownComponent.vue";

export default {
  setup() {
    const state = reactive({
      value: "",
      items: [
        "Russia",
        "USA",
        "Canada",
        "Australia",
        "New Zealand",
        "India",
        "China",
        "Japan",
        "Korea",
        "Taiwan",
        "Germany",
        "France",
      ],
    });

    return state;
  },

  name: "CountryDropdown",
  components: {
    DropdownComponent,
  },
};
</script>
