<template>
  <div class="w-64">
    <button
      class="dropdown w-64 py-2 px-4 text-sm border text-left focus:outline-none focus:border-yellow-500 focus:border-1 flex justify-between items-center"
      @click="toggleDropdown"
    >
      {{ modelValue ? modelValue : placeholder }}

      <i
        class="transition linear duration-300"
        :class="{ 'rotate-180': state.isDropdownOpen }"
      >
        <svg
          width="12"
          height="7"
          viewBox="0 0 12 7"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            fill-rule="evenodd"
            clip-rule="evenodd"
            d="M11.7071 6.70711C11.3166 7.09763 10.6834 7.09763 10.2929 6.70711L6 2.41421L1.70711 6.70711C1.31658 7.09763 0.683417 7.09763 0.292893 6.70711C-0.0976315 6.31658 -0.0976315 5.68342 0.292893 5.29289L5.29289 0.292893C5.68342 -0.097631 6.31658 -0.097631 6.70711 0.292893L11.7071 5.29289C12.0976 5.68342 12.0976 6.31658 11.7071 6.70711Z"
            fill="#253238"
          />
        </svg>
      </i>
    </button>
    <div
      v-show="state.isDropdownOpen"
      class="py-2 absolute w-full mt-2 rounded z-50 overflow-auto max-h-52 shadow-xl"
    >
      <div
        v-for="(item, index) in items"
        :key="index"
        @click="handleSelect(item)"
        class="block text-left py-2.5 px-4 text-base font-normal hover:bg-[#FFF9F4] active:bg-[#FF9A4D] active:text-white active:cursor-pointer"
      >
        {{ item }}
      </div>
    </div>
  </div>
</template>

<script>
import { reactive } from "vue";
export default {
  name: "DropdownComponent",
  props: {
    placeholder: String,
    items: Array,
    type: String
    modelValue: String,
  },

  setup(props, context) {
    const state = reactive({
      isDropdownOpen: false,
    });

    const handleSelect = (item) => {
      context.$emit("update:modelValue", item);
      state.isDropdownOpen = false;
    };

    const toggleDropdown = () => {
      state.isDropdownOpen = !state.isDropdownOpen;
    };

    return {
      state,
      handleSelect,
      toggleDropdown,
    };
  },
};
</script>

<style scoped>
::-webkit-scrollbar {
  width: 8px;
}
::-webkit-scrollbar-thumb {
  background-color: #d0d9de;
  border-radius: 15px;
  position: absolute;
}
</style>
