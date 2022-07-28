<template>
  <div class="w-64">
    <button
      class="dropdown w-64 py-2 px-4 text-sm border text-left focus:outline-none focus:border-yellow-500 focus:border-1 flex justify-between items-center"
      @click="toggleDropdown"
    >
      <div>
        <div v-if="type === DropdownTypes.MULTISELECT" class="flex items-center gap-1">
          <span
            v-if="modelValue.length > 0"
            v-for="(item, index) in modelValue"
            :key="index"
            class="flex items-center gap-[2px]"
          >
            {{ item }}

            <div @click="handleDeselect(item)">
              <svg
                width="11"
                height="11"
                viewBox="0 0 11 11"
                fill="none"
                xmlns="http://www.w3.org/2000/svg"
              >
                <path
                  d="M10.0215 1.02861L9.01432 0.0214657L5.02147 4.01432L1.02861 0.0214657L0.0214657 1.02861L4.01432 5.02147L0.0214657 9.01432L1.02861 10.0215L5.02147 6.02861L9.01432 10.0215L10.0215 9.01432L6.02861 5.02147L10.0215 1.02861Z"
                  fill="#FFBC0F"
                />
              </svg>
            </div>
          </span>
          <span v-else>
            {{ placeholder }}
          </span>
        </div>

        <div v-if="type === DropdownTypes.SELECT">
          <span>
            {{ modelValue || placeholder }}
          </span>
        </div>
      </div>

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
        class="flex items-center justify-between text-left py-2.5 px-4 text-base font-normal hover:bg-[#FFF9F4] active:bg-[#FF9A4D] active:text-white active:cursor-pointer"
      >
        {{ item }}
        <input
          v-show="type === 'multiselect'"
          type="checkbox"
          :id="`checkbox-${index}`"
          :value="item"
          :checked="modelValue.includes(item)"
          @change="handleChange"
        />
      </div>
    </div>
  </div>
</template>

<script>
import { reactive } from "vue";

const DropdownTypes = {
  SELECT: "select",
  MULTISELECT: "multiselect",
};

export default {
  name: "DropdownComponent",
  props: {
    placeholder: String,
    items: Array,
    type: {
      type: String,
      default: DropdownTypes.SELECT,
    },
    modelValue: String | Array,
  },
  emits: ["update:modelValue"],

  setup(props, { emit }) {
    const state = reactive({
      isDropdownOpen: false,
    });

    const handleSelect = (item) => {
      if (props.type === DropdownTypes.MULTISELECT) return;
      emit("update:modelValue", item);
      state.isDropdownOpen = false;
    };

    const handleChange = (e) => {
      const checked = e.target.checked;
      const value = e.target.value;
      let newModele = props.modelValue || [];
      if (checked) {
        newModele.push(value);
      } else {
        newModele = newModele.filter((item) => item !== value);
      }
      emit("update:modelValue", newModele);
    };

    const handleDeselect = (item) => {
      const newModele = props.modelValue.filter((itm) => itm !== item);
      emit("update:modelValue", newModele);
    };
    const toggleDropdown = () => {
      state.isDropdownOpen = !state.isDropdownOpen;
    };

    return {
      state,
      handleSelect,
      toggleDropdown,
      handleChange,
      handleDeselect,
      DropdownTypes
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
