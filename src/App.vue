<template>
  <div id="app">
    <img src="https://mcvictormurillo.github.io/WebSiteVueJS/dist/logo.png">
    <h1>APP MUSIC</h1>
    
    <select v-model="selectedCountry" >
      <option v-for="country in countries" v-bind:value="country.value">{{country.name}}</option>
    </select>

    <spinner v-show="loading"> </spinner>
    <ul>
      <artist v-for="artist in artists" v-bind:artist="artist"
      v-bind:key="artist.mbid"></artist>
      
    </ul>
  </div>
</template>

<script>
import Spinner from './components/Spinner.vue'
import Artist from './components/Artist.vue'
import  getArtists from './api/index'
export default {
  name: 'app',
  data () {
    return {
      artists:[],
      selectedCountry:'argentina',
      countries:[
        {name:'Argentina',value:'argentina'},
        {name:'Colombian',value:'colombia'},
        {name:'Espania',value:'spain'},
      ],
      loading: true
    }
  },
  components:{
    Artist,
    Spinner
  },
  methods: {
    refreshArtists(){
    const self = this
    this.loading = true
    getArtists(this.selectedCountry)
    .then(function(arts){
      self.loading = false
      self.artists = arts
      console.log(`los artistas son ${self.artists}`)
    })
    }
  },
  mounted: function() {
    this.refreshArtists()
  },
  watch: {
    selectedCountry: function(){
      this.refreshArtists()
    }
  },
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: red;
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
