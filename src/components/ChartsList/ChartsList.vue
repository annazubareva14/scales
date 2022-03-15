<template>
  <div>
    <div v-for="(scale, ind) of scales" :key="ind" class="scale">
      <h3 class="scale__title">
        {{ scale.title }}
      </h3>
      <div class="scale__bar__wrapper">
        <charts-bar
          :greenSectionCount="scale.greenSectionCount"
          :yellowSectionCount="scale.yellowSectionCount"
          :redSectionCount="scale.redSectionCount"
        />
      </div>
    </div>
  </div>
</template>

<script>
import ChartsBar from "@/components/ChartsBar/ChartsBar.vue";
import data from "./mocks.json";
export default {
  name: "ChartsList",

  components: { ChartsBar },

  data() {
    return {
      scales: data,
    };
  },
};
</script>

<style lang="scss">
.scale {
  display: inline-flex;
  margin-right: 40px;
  &__title {
    font-size: 16px;
    margin-right: 15px;
  }

  &__bar__wrapper {
    align-self: center;
  }
}
</style>
