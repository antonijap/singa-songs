<template>
  <div id="app">
  <div class="checkbox-div">
  	<!-- this iterates the languages and passes each as an prop for a FilterCheckbox component -->
		<FilterCheckbox v-for="lang in languages" :data="lang" :key="lang.code"/>
	</div>

	  <div class="row songs">
	  	<transition-group name="list-complete" >
	    	<div v-if="songs.length >0" class="col-3 list-complete-item" v-for="song in songs" :key="song.id">
	    	<!-- this iterates the songs and passes props for the Song component -->
		  		<Song :title="song.name" :artist="song.artists[0].name" :image="song.image.tiny.url" :genre=	"song.genres[0].name"/> 
	  		</div>
	  </transition-group>
  </div>
  </div>
</template>

<script>
  import Song from './components/Song'
  import DropdownButton from './components/DropdownButton'
  import FilterCheckbox from './components/FilterCheckbox'
  import Axios from 'axios'
  
  const requestSongsFromApi = (filters) => {
  		//fancy javascript one liners
				var filtersAsString = Object.keys(filters).map(filter => filter+"="+filters[filter].join(",")).join("&")
				//make the axios request with the given parameters
				return Axios.get(`https://api.sin.ga/v1.4/songs/?page_size=20&${filtersAsString}`)
    	}
  
  export default {
    name: 'App',
    components: {
      Song,
      DropdownButton,
      FilterCheckbox
    },
    data () {

    	return {
    		songs: [],
    		filters: {
    			language:[],
    			sort: ["top"]
    		},
    		languages: {
    			"en":{	
    				code:"en",
    				name: "English",
    				active: true
    			},
    			"fi":{
    				code:"fi",
    				name: "Finnish",
    				active: false
    			},
    			"sv":{	
    				code:"sv",
    				name: "Swedish",
    				active: false
    			},
    			"de":{
    				code:"de",
    				name: "German",
    				active: false
    			}
    		}
    			
  		}
    },
   beforeCreate () {
			
  	},
  	created () {
  		requestSongsFromApi(this.filters).then(res=>{
    		this.songs = res.data.results
    	})

  		//a listener is set for the $emit event in FilterCheckbox.vue
  		this.$root.$on("setLanguage", (value) => {
  			//set the value of language object that was emitted
  			this.languages[value.key].active  = value.active

  			//maps the objects to a array of language codes 
  			this.filters.language = Object.keys(this.languages).map(lang=>this.languages[lang]).filter(lang=>lang.active).map(lang => lang.code)

  			//do new request
  			requestSongsFromApi(this.filters).then(res=>{
		  		this.songs = res.data.results
		  	})
  		})


  	},
    methods: {
    	requestSongs () {
				requestSongsFromApi(this.filters).then(res=>{
		    		this.songs = res.data.results
		    	})
    	}

    }
}
</script>
<style lang="scss" scoped>
		.checkbox-div {
			margin: 30px 0 30px 0;
		}
		.col-3 {
			  display: inline-flex;
		}

		.list-complete-item {
			transition: all 1s;
		}
		.list-complete-enter{
			transform: scaleX(0);
		  opacity: 0;
		  transition: all 1s;
		}
		.list-complete-leave-to {
			transform: scaleX(0);
		  opacity: 0;
		  width: 0px;
		  transition: all 1s;

		}

		
		.list-complete-leave, list-complete-enter-to{
			opacity: 1;
		  transition: all 1s;
		}
	</style>
