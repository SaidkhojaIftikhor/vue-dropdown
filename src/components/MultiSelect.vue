<template>
  <DropdownComponent
    v-model="value"
    :items="items"
    placeholder="Select country"
    :type="type"

  />
</template>

<script>
import { reactive } from "vue";
import DropdownComponent from "./DropdownComponent.vue";

export default {
  name: "CountryDropdown",
  components: {
    DropdownComponent,
  },
  
  setup() {
    const state = reactive({
      value: "",
      items: [
        "one",
        "two",
        "three",
        "four",
      ],
      type: 'multiselect'
    });

    return state;
  },
};
</script>
