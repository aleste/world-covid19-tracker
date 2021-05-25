<template>
 <main v-if="!loading">
   <DataTitle :title="title" :dataDate="dataDate"/>
   <DataBoxes :stats="stats"/>
   <CountrySelect :countries="countries" @get-country="getCountryData" />
  <button v-if="stats.Country" @click="clearCountryData" class="bg-green-700 text-white rounded p-3 mt-10 focus:outline-none hover:bg-gree-600">Clear Country</button>
 </main>
 <main class="flex flex-col align-center justify-center text-center" v-else>
   <div class="text-grey-500 text-3xl mt-10 mb-6"> Fetching data...</div>
 </main>
</template>

<script>

import DataTitle from '@/components/DataTitle.vue'
import DataBoxes from '@/components/DataBoxes.vue'
import CountrySelect from '@/components/CountrySelect.vue'
export default {
  name: 'Home',
  components: { DataTitle, DataBoxes, CountrySelect },
  data() {
    return {
      loading: true,
      title: 'Global',
      dataDate: null,
      stats: {},
      countries: [],
    }
  },
  methods: {
    async fetchCovidData () {
      const res = await fetch('https://api.covid19api.com/summary')
      return await res.json()
    },
    getCountryData (country) {
      this.stats = country
      this.title = country.Country
    },
    async clearCountryData(){
      this.loading = true
      const data = await this.fetchCovidData()
      this.title = 'Global'
      this.stats = data.Global
      this.loading = false
    }
  },
  async created() {
    const data = await this.fetchCovidData()
    this.dataDate = data.dataDate
    this.stats = data.Global
    this.countries = data.Countries
    this.loading = false
  }
}
</script>
