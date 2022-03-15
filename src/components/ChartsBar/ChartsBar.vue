<template>
  <div class="bar">
    <charts-section
      class="section--green"
      :section-count="greenSectionCount"
      @hover="onSectionHover"
      @out="onSectionOut"
    />
    <charts-section
      class="section--yellow"
      :section-count="yellowSectionCount"
      @hover="onSectionHover"
      @out="onSectionOut"
    />
    <charts-section
      class="section--red"
      :section-count="redSectionCount"
      @hover="onSectionHover"
      @out="onSectionOut"
    />
    <charts-section
      class="section--gray"
      :section-count="getGraySectionCount"
      @hover="onSectionHover"
      @out="onSectionOut"
    />
  </div>
</template>

<script>
import ChartsSection from "./ChartsSection.vue";
import { TOTAL_COUNT } from "./helper.js";

export default {
  name: "ChartsBar",

  components: { ChartsSection },

  props: {
    greenSectionCount: {
      type: Number,
      default: 0,
    },
    yellowSectionCount: {
      type: Number,
      default: 0,
    },
    redSectionCount: {
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
    getGraySectionCount() {
      return (
        this.totalCount -
        (this.greenSectionCount +
          this.yellowSectionCount +
          this.redSectionCount)
      );
    },
  },
};
</script>

<style lang="scss">
.bar {
  cursor: pointer;
  display: inline-flex;
  width: 300px;
  border-radius: 5px;
  overflow: hidden;
  border: 1px #fff solid;
}

.section--green {
  background-color: #45e596;
}

.section--yellow {
  background-color: #ffc44c;
}

.section--red {
  background-color: #ff4c4c;
}

.section--gray {
  background-color: #f2f2f2;
}
</style>
