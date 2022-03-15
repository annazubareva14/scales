<template>
  <div
    :style="getStyledSectionWidth"
    class="section"
    @mouseover="toggleClassHover"
    @mouseleave="toggleClassHoverOut"
  />
</template>

<script>
import { TOTAL_COUNT } from "./helper.js";

export default {
  name: "ChartsSection",

  props: {
    sectionCount: {
      type: Number,
      default: 0,
    },

    color: {
      type: String,
      default: "",
    },
  },

  data() {
    return {
      totalCount: TOTAL_COUNT,
    };
  },

  computed: {
    getSectionWidth() {
      return (this.sectionCount / this.totalCount) * 100;
    },

    getStyledSectionWidth() {
      return `width: ${this.getSectionWidth}%;`;
    },
  },

  methods: {
    toggleClassHover() {
      this.$emit("hover", this.color);
    },

    toggleClassHoverOut() {
      this.$emit("hoverOut", this.color);
    },
  },
};
</script>

<style lang="scss">
.section {
  min-width: 8px;
  width: 0px;
  height: 6px;
  box-shadow: -1px 0px 0px 0px #fff inset;

  &:last-child {
    box-shadow: none;
  }
}
</style>
