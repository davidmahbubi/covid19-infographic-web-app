<template>
  <div class="home">
    <div class="container">
      <highlight-stats class="highlight-stats"/>
      <statistic-per-country class="table-statistics-row" />
    </div>
  </div>
</template>

<script>

import HighlightStats from '@/components/HighlightStats.vue';
import StatisticPerCountry from '@/components/StatisticPerCountry.vue';

export default {
  name: 'Home',
  components: {
    HighlightStats,
    StatisticPerCountry
  },
  methods: {
    changeLoc(e) {
      console.log(e.target.value);
    }
  }
};
</script>

<style scoped>

.highlight-stats {
  margin-top: 28px;
}

.paginate_button {
  background-color: red !important;
}

.table-statistics-row {
  margin-top: 30px
}

</style>
