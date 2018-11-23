<template>
  <div id="app">
    <img src="https://dprietoc.github.io/vueSampleLastfmAPI/dist/logo.png">
    <h1>App Platzi Music</h1>
    <select name="countries" id="countries" v-model="selectedCountry">
      <option v-for="country in countries" :value="country.value">{{country.name}}</option>
    </select>
    <Spinner v-show="loading"></Spinner>
    <ul v-show="!loading">
      <artist v-for="artist in artists" :artist='artist' :key="artist.mbid"></artist>
    </ul>
  </div>
</template>

<script>
import getArtist from './api';
import Artist from './components/Artist.vue'
import Spinner from './components/Spinner.vue'

export default {
  name: 'app',
  data () {
    return {
      artists: [],
      countries: [
        { name: 'Argentina', value: 'argentina' },
        { name: 'Uruguay', value: 'uruguay' },
        { name: 'España', value: 'spain' },
      ],
      selectedCountry: 'argentina',
      loading: true
    }
  },
  methods: {
    refreshArtist(){
        const self = this
        this.loading = true
        getArtist(this.selectedCountry).then(function(artists){
          self.artists = artists;
        }).finally(function(){ self.loading = false })
    }
  },
  components: {
    Artist,
    Spinner
  },
  mounted () {
    this.refreshArtist();
  },
  watch: {
    selectedCountry: function(){
      this.refreshArtist();
    }
  }
}
</script>

<style lang="scss" scoped>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
