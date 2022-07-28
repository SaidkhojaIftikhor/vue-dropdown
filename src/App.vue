<script>
import CountryDropdown from "./components/CountryDropdown.vue";
import MultiSelect from "./components/MultiSelect.vue";
export default {
  name: "App",
  components: {
    CountryDropdown,
    MultiSelect,
  },
};
</script>

<template>
  <main class="flex justify-center gap-10 mt-20">
    <CountryDropdown />
    <MultiSelect />
  </main>
</template>
