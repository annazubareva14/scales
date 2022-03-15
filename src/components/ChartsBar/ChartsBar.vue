<template>
  <div class="bar">
    <charts-section
      v-if="greenSectionCount > 0"
      class="section--green"
      :section-count="greenSectionCount"
      color="green"
      ref="green"
      @hover="onSectionHover"
      @hoverOut="onSectionHoverOut"
    />
    <charts-section
      v-if="yellowSectionCount > 0"
      class="section--yellow"
      :section-count="yellowSectionCount"
      ref="yellow"
      color="yellow"
      @hover="onSectionHover"
      @hoverOut="onSectionHoverOut"
    />
    <charts-section
      v-if="redSectionCount > 0"
      class="section--red"
      :section-count="redSectionCount"
      ref="red"
      color="red"
      @hover="onSectionHover"
      @hoverOut="onSectionHoverOut"
    />
    <charts-section
      v-if="graySectionCount > 0"
      class="section--gray"
      :section-count="graySectionCount"
      ref="gray"
      color="gray"
      @hover="onSectionHover"
      @hoverOut="onSectionHoverOut"
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
  },

  data() {
    return {
      totalCount: TOTAL_COUNT,
      colors: ["green", "yellow", "red", "gray"],
    };
  },

  computed: {
    graySectionCount() {
      return (
        this.totalCount -
        (this.greenSectionCount +
          this.yellowSectionCount +
          this.redSectionCount)
      );
    },
  },

  methods: {
    onSectionHover(color) {
      this.colors.forEach((color) => {
        if (this.$refs[color]) {
          this.$refs[color].$el.classList.add("transparent");
        }
      });
      this.$refs[color].$el.classList.add("hovered");
    },

    onSectionHoverOut(color) {
      this.colors.forEach((color) => {
        if (this.$refs[color]) {
          this.$refs[color].$el.classList.remove("transparent");
        }
      });
      this.$refs[color].$el.classList.remove("hovered");
    },
  },
};
</script>

<style lang="scss">
.bar {
  cursor: pointer;
  display: inline-flex;
  width: 255px;
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

.transparent {
  opacity: 0.08;
}

.hovered {
  opacity: 1;
}
</style>
