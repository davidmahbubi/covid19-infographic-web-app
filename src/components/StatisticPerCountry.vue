<template>
    <div class="row">
        <div class="col12">
            <h5>Statistik per Negara</h5>
            <div class="row sort-form-row">
                <div class="input-field col s12">
                    <select name="" v-model="sortBy">
                        <option value="confirmed">Kasus</option>
                        <option value="recovered">Sembuh</option>
                        <option value="deaths">Meninggal</option>
                    </select>
                    <label for="">Urutkan Dari</label>
                </div>
            </div>
            <div class="row" v-if="countriesListCases.length > 0">
              <div class="col12">
                <table class="highlight">
                  <thead>
                    <tr>
                        <th>#</th>
                        <th>Negara</th>
                        <th>Kasus 😢 </th>
                        <th>Sembuh 😃</th>
                        <th>Meninggal 😭</th>
                    </tr>
                  </thead>
                  <tbody>
                    <tr v-for="i in limit" :key="i">
                      <td>{{ i }}</td>
                      <td>{{ `${countriesListCases[i].countryRegion} ${countriesListCases[i].provinceState ? `(${countriesListCases[i].provinceState})` : ''}` }}</td>
                      <td>{{ formatNumber(countriesListCases[i].confirmed) }}</td>
                      <td>{{ formatNumber(countriesListCases[i].recovered) }}</td>
                      <td>{{ formatNumber(countriesListCases[i].deaths) }}</td>
                    </tr>
                  </tbody>
                </table>
                <a href="" class="waves-effect" @click.prevent="loadMore">Muat Lebih Banyak</a>
              </div>
            </div>
        </div>
    </div>
</template>

<script>

import Axios from 'axios';
import Numeral from 'numeral';

export default {
  data() {
    return {
      countriesList: [],
      selectedCountry: '',
      countriesListCases: [],
      limit: 5,
      sortBy: 'confirmed',
    };
  },
  mounted() {
    var elems = document.querySelectorAll('select');
    var instances = M.FormSelect.init(elems);
  },
  created() {
    this.fetchCountryList();
    this.fetchCountriesCase(this.sortBy);
  },
  methods: {
    async fetchCountryList() {
      const { data } = await Axios.get('https://covid19.mathdro.id/api/countries');
      this.countriesList = data.countries;
    },
    async fetchCountriesCase(by) {
      this.countriesList = [];
      const { data } = await Axios.get(`https://covid19.mathdro.id/api/${by}`);
      this.countriesListCases = data;
    },
    formatNumber(number) {
      return Numeral(number).format('0,0');
    },
    loadMore() {
      this.limit += 5;
    }
  },
  computed: {
    fetchCountries() {
      return this.countriesList;
    }
  },
  watch: {
    sortBy(val) {
      this.fetchCountriesCase(val);
    },
  },
}
</script>

<style scoped>

.sort-form-row {
  margin-top: 25px;
  margin-bottom: 0
}

.highlight {
  margin-bottom: 20px;
}

</style>