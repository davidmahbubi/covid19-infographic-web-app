<template>
  <div class="about">
    <div class="container about-container">
      <h4 class="deep-orange-text">
        Covid 19 Information Web
      </h4>
      <span>Made with ❤ by <a href="https://mhbproject.com" target="blank">MHB Project</a></span>
      <div class="credit">
        <ul>
          <li>Version : 2.0.0</li>
          <li>Covid 19 Data API : <a href="https://github.com/mathdroid/covid-19-api">Mathdroid</a></li>
          <li>Data Last Update : {{ getLastUpdate }}</li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>

import Axios from 'axios';

export default {
  data() {
    return {
      lastUpdate: ''
    }
  },
  created() {
    this.fetchUpdated();
  },
  methods: {
    async fetchUpdated() {
      const { data } = await Axios.get('https://covid19.mathdro.id/api');
      this.lastUpdate = data.lastUpdate;
    },
  },
  computed: {
    getLastUpdate() {
      return this.lastUpdate;
    },
  },
}
</script>

<style scoped>

.about-container {
  text-align: center;
  margin-top: 60px;
}

.credit {
  margin: 50px 0;
}
</style>
