<template>
  <div
    :style="getStyledSectionWidth"
    v-if="isSectionVisible"
    :class="[{ hovered: isSectionHovered }, 'section']"
    @mouseover="toggeClassHover"
    @mouseleave="toggeClassHoverOut"
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

    isSectionHovered: {
      type: Boolean,
      default: false,
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
    isSectionVisible() {
      return this.sectionCount > 0;
    },
  },

  methods: {
    toggeClassHover() {
      this.$emit("hover");
    },

    toggeClassHoverOut() {
      this.$emit("hoverOut");
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

// .section:not(.hovered) {
//   opacity: 40%;
// }
</style>
