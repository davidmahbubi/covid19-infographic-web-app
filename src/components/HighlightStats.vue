<template>
    <div id="highilight-stats">
        <h5 class="current-location-info">Data di {{ indonesianData ? 'Indonesia' : 'Seluruh Dunia' }}</h5>
        <div class="switch">
            <label>
                <input type="checkbox" v-model="indonesianData" checked>
                <span class="lever"></span>
            </label>
        </div>
        <div class="row highlight-card-row">
            <div class="col s12 m6 l4">
                <high-light-card
                  title="Kasus"
                  icon="fa-frown"
                  :value="`${highlight.case} orang`"
                  color="purple"
                />
            </div>
            <div class="col s12 m6 l4">
                <high-light-card
                  title="Sembuh"
                  icon="fa-smile"
                  :value="`${highlight.recovered} orang`"
                  color="green"
                />
            </div>
            <div class="col s12 m6 l4">
                <high-light-card
                  title="Meninggal"
                  icon="fa-sad-cry"
                  :value="`${highlight.deaths} orang`"
                  color="red"
                />
            </div>
        </div>
    </div>
</template>

<script>

import Axios from 'axios';
import Numeral from 'numeral';
import HighLightCard from '@/components/HighlightCard.vue';

export default {
  data() {
    return {
      highlight: {
        case: '',
        recovered: '',
        deaths: '',
      },
      indonesianData: true,
    };
  },
  created() {
    this.toggleLoading(true);
    this.fetchApiData();
  },
  components: {
    HighLightCard,
  },
  methods: {
    async fetchApiData() {
      this.toggleLoading(true);
      if (this.indonesianData) {
          const { data } = await Axios.get('https://covid19.mathdro.id/api/countries/Indonesia');
          this.setHighlightValue(data);
      } else {
          const { data } = await Axios.get('https://covid19.mathdro.id/api');
          this.setHighlightValue(data);
      }
    },
    setHighlightValue({ confirmed, recovered, deaths }) {
      this.highlight.case = Numeral(confirmed.value).format('0,0');
      this.highlight.recovered = Numeral(recovered.value).format('0,0');
      this.highlight.deaths = Numeral(deaths.value).format('0,0');
    },
    toggleLoading(state) {
      if (state) {
        this.highlight = {
          case: '...',
          recovered: '...',
          deaths: '...',
        };
      };
    },
  },
  watch: {
    indonesianData() {
      this.fetchApiData();    
    }
  }
}
</script>

<style scoped>

.highlight-card-row {
    margin-top: 16px;
}

.switch {
    float: right;
}

.current-location-info {
    display: inline;
}

</style>