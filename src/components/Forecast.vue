<template>
  <div>
    <br />
    <b-list-group v-for="(l, i) of forecast.list" :key="i">
      <b-list-group-item>
        <b>Date: {{l.dt_txt}}</b>
      </b-list-group-item>
      <b-list-group-item>Temperature: {{l.main.temp - 273.15}} C</b-list-group-item>
      <b-list-group-item>High: {{l.main.temp_max - 273.15}} C</b-list-group-item>
      <b-list-group-item>Low: {{l.main.temp_min }}mb</b-list-group-item>
      <b-list-group-item>Pressure: {{l.main.pressure }}mb</b-list-group-item>
    </b-list-group>
  </div>
</template>

<script>
import { requestsMixin } from "@/mixins/requestsMixin";
import store from "../store";
import { BListGroup, BListGroupItem } from "bootstrap-vue";
import 'bootstrap/dist/css/bootstrap.css'
import 'bootstrap-vue/dist/bootstrap-vue.css'

export default {
  store,
  name: "Forecast",
  mixins: [requestsMixin],
  components: {
    BListGroup,
    BListGroupItem
  },
  computed: {
    keyword() {
      return this.$store.state.keyword;
    }
  },
  data() {
    return {
      forecast: []
    };
  },
  watch: {
    async keyword(val) {
      const response = await this.searchForecast(val);
      this.forecast = response.data;
    }
  }
};
</script>

<style scoped>
p {
  font-size: 20px;
}
</style>
