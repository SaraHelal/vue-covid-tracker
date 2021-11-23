<template>
  <main v-if="!loading">
    
    <DataTitle :title = 'title' :dateData = 'dateData' />
    <DataBoxes :stats = 'stats'/>
    <CountrySelect :countries = 'countries' @get-country="changeCountry"/>
    <button v-if="stats.Country" @click="clearSelected" class="bg-green-700 text-white rounded p-3 mt-10 hover:bg-green-600 focus:outline-none">Clear Country</button>
  </main>
  <main v-else class="flex flex-col align-center justify-center text-center ">
    <div class="text-gray-500 text-3xl mt-10 mb-6">Fetching Data</div>
    <img :src="loadingImage" class="w-24 mx-auto" alt="loading image">
  </main>
</template>

<script>
import DataTitle from '../components/DataTitle'
import DataBoxes from '../components/DataBoxes'
import CountrySelect from '../components/CountrySelect'

export default {
  name: 'Home',
  data(){
    return{
      loading: true,
      title: 'Global',
      dateData: '',
      countries : [],
      stats: {},
      loadingImage: require('../assets/hourglass.gif'),
    }
  },
  components: {
    DataTitle,
    DataBoxes,
    CountrySelect
  },
  methods:{
    async fetchCovidData(){
      const res = await fetch('https://api.covid19api.com/summary');
      const data = await res.json();
      return data; 
    },
    changeCountry(country){
      this.title = country.Country;
      this.stats = country;
    },
    async clearSelected(){
      this.loading = true;
      const data = await this.fetchCovidData();
      this.title = 'Global';
      this.stats = data.Global ;
      this.loading = false;
       
    }
    
  },
  async created(){
    const data = await this.fetchCovidData();
    this.dateData = data.Date;
    this.countries = data.Countries;
    this.stats = data.Global;
    this.loading = false;

    //console.log(this.dateData);

  },
  computed:{
    
  },
  emits:['country'],
}
</script>
