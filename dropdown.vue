<template>
  <div class="relative inline-flex align-middle w-full dropdown-wrapper">
    <button
      :class="`${opts.textColor || 'text-white'} font-normal ${
        opts.upperCase && 'uppercase'
      } text-xs px-6 py-1 rounded ${opts.shadow && 'shadow'} ${
        opts.hoverClasses
      } mr-1 mb-1 outline-none focus:outline-none ${opts.backgroundColor || 'bg-gray-800'}`"
      style="transition: all 0.15s ease"
      type="button"
      v-on:click="toggleDropdown()"
      ref="btnDropdownRef"
    >
      <unicon
        :name="icon"
        fill="currentColor"
        :class="`-mb-2 ${opts.iconClacces}`"
        :height="`${opts.iconH||24}`"
        :width="`${opts.iconW||24}`"
        v-if="icon"
      />
      {{ text }}
    </button>
    <div
      v-bind:class="{
        hidden: !dropdownPopoverShow,
        block: dropdownPopoverShow,
      }"
      class="bg-white text-base z-50 float-left py-2 list-none text-left rounded shadow-lg mt-1 dropdown"
      style="min-width: 12rem"
      ref="popoverDropdownRef"
    >
      <slot></slot>

      <!-- <div class="h-0 my-2 border border-solid border-t-0 border-gray-900 opacity-25"></div> -->
    </div>
  </div>
</template>

<script>
import Popper from "popper.js";

export default {
  name: "dropdown",
  props: ["text", "icon", "options"],
  data() {
    return {
      dropdownPopoverShow: false,
      default: {
        textColor: "text-white",
        shadow: true,
        upperCase: false,
        backgroundColor: "bg-gray-800",
        iconClacces: "",
        iconW: 24,
        iconH: 24,
        hoverClasses: "hover:shadow-lg",
      },
    };
  },
  computed: {
    opts() {
      if (this.options) {
        for (var propertyName in this.default)
          this.default[propertyName] &&
            (this.default[propertyName] = this.options[propertyName]);
      }
      return this.default;
    },
  },
  methods: {
    toggleDropdown: function () {
      if (this.dropdownPopoverShow) {
        this.dropdownPopoverShow = false;
      } else {
        this.dropdownPopoverShow = true;
        new Popper(this.$refs.btnDropdownRef, this.$refs.popoverDropdownRef, {
          placement: "bottom-start",
        });
      }
    },
  },
};
</script>