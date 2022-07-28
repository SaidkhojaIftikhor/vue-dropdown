<script>
import CountryDropdown from "./components/CountryDropdown.vue";

export default {
  name: "App",
  components: {
    CountryDropdown,
  },
};
</script>

<template>
  <main class="flex justify-center mt-20">
    <CountryDropdown />
  </main>
</template>
