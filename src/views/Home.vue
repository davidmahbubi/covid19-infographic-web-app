<template>
  <div class="home">
    <div class="container">
      <highlight-stats class="highlight-stats"/>
      <statistic-per-country class="table-statistics-row" />
      <div class="fixed-action-btn">
        <a href="" class="btn-floating btn-large waves-effect waves-light red fixed-action-btn">
          <i class="large material-icons">favorite</i>
        </a>
      </div>
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
  mounted() {
    var elems = document.querySelectorAll('.fixed-action-btn');
    var instances = M.FloatingActionButton.init(elems);
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
