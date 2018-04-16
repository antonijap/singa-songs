<template>
  <div id="app">
		<div class="row">
			<div class="col-auto">
					<DropdownButton :title="'Languages'" :filterData="languages" filterDataType="language"/>
			</div>
			<div class="col-auto">
					<DropdownButton :title="'Genres'" :filterData="genres" filterDataType="genre"/>
			</div>
		</div>

		<div class="row filters">
			<div class="col-auto">
					<SelectedFilter  v-for="lang in selectedLanguages" :dataObj="lang" :key="lang.id" @click="deleteFilter('language', lang.id)" dataType="language"/>

			</div>
			<div class="col-auto">
					<SelectedFilter  v-for="genre in selectedGenres" :dataObj="genre" :key="genre.id" dataType="genre"/>
			</div>
		</div>

  <div class="checkbox-div">
  	<!-- this iterates the languages and passes each as an prop for a FilterCheckbox component -->
		
	</div>
		<LoadingSpinner v-if="loading"/>
		
	  <div v-else class="row songs">
	    	<div v-if="songs.length >0" class="col-6 col-sm-4 col-md-3 col-lg-2 list-complete-item" v-for="song in songs" :key="song.id">

	    	<!-- this iterates the songs and passes props for the Song component -->
		  		<Song :title="song.name" :artist="song.artists[0].name" :image="song.image.small.url" :genre=	"song.genres.map(genre => genre.name).join(', ')"/> 
	  		</div>
  </div>
  </div>
</template>

<script>
  import Song from './components/Song'
  import DropdownButton from './components/DropdownButton'
  import FilterCheckbox from './components/FilterCheckbox'
	import SelectedFilter from './components/SelectedFilter'
	import LoadingSpinner from './components/LoadingSpinner'
  import Axios from 'axios'
  
  const requestSongsFromApi = (filters) => {
	//fancy javascript one liners
		var filtersAsString = Object.keys(filters).map(filter => filter+"="+filters[filter].join(",")).join("&")
		//make the axios request with the given parameters
		return Axios.get(`https://api.sin.ga/v1.4/songs/?page_size=20&${filtersAsString}`)
	}
	const getGenres = () => {
	//fancy javascript one liners
		
		//make the axios request with the given parameters
		return Axios.get(`https://api.sin.ga/v1.4/genres/?page_size=100`)
	}
  
  export default {
    name: 'App',
    components: {
      Song,
      DropdownButton,
			SelectedFilter,
      FilterCheckbox,
      LoadingSpinner
    },
    data () {

    	return {
    		loading: false,
    		songs: [],
    		filters: {
    			genre: [],
    			language:[],
    			sort: ["top"]
    		},
    		languages: {
    			"en":{	
    				id:"en",
    				name: "English",
    				active: false
    			},
    			"fi":{
    				id:"fi",
    				name: "Finnish",
    				active: false
    			},
    			"sv":{	
    				id:"sv",
    				name: "Swedish",
    				active: false
    			},
    			"de":{
    				id:"de",
    				name: "German",
    				active: false
    			},
    			"he":{
    				id:"he",
    				name: "Hebrew",
    				active: false
    			},
    			"it":{
    				id:"it",
    				name: "Italian",
    				active: false
    			},
    			"fr":{
    				id:"fr",
    				name: "French",
    				active: false
    			},
    			"ko":{
    				id:"ko",
    				name: "Korean",
    				active: false
    			}
    		},
    		genres : {}		
  		}
    },
   beforeCreate () {
			getGenres().then(res => {
				res.data.results.forEach(genre => {
					this.$set(this.genres,genre.id,  {
						id: genre.id,
						name: genre.name,
						active: false
					})
				})
			})
  	},
  	created () {
  		requestSongsFromApi(this.filters).then(res=>{
    		this.songs = res.data.results
    	})

  		//a listener is set for the $emit event in FilterCheckbox.vue
  		this.$root.$on("setFilter", (value) => {
  			const obj = value.type === "genre" ? this.genres : this.languages
  			//set the value of language object that was emitted
  			obj[value.key].active  = value.active

  			//maps the objects to a array of language ids 
  			this.filters[value.type] = Object.keys(obj).map(lang=>obj[lang]).filter(lang=>lang.active).map(lang => lang.id)

  			//do new request
  			this.loading = true
  			requestSongsFromApi(this.filters).then(res=>{
		  		this.songs = res.data.results
		  		this.loading = false
		  	})
  		})


  	},
  	computed: {
  		selectedGenres() {
  			return Object.keys(this.genres).map(key => this.genres[key]).filter(genre => genre.active)
  		},
  		selectedLanguages () {
  			return Object.keys(this.languages).map(key => this.languages[key]).filter(language => language.active)
  		},

  	},
    methods: {
    	requestSongs () {
    		this.loading = true
				requestSongsFromApi(this.filters).then(res=>{
		    		this.songs = res.data.results
		    		this.loading = false
		    	})
    	},
    	deleteFilter(type, id) {
    		const obj = value.type === "genre" ? this.genres : this.languages
  			//set the value of language object that was emitted
  			obj[id].active  = false

    	}

    }
}
</script>
<style lang="scss" scoped>
		.songs{
			z-index: 1;
		}
		.checkbox-div {
			margin: 30px 0 30px 0;
		}
		.list-complete-item {
			transition: transform 1s;
		}
		.list-complete-enter{
			transform: scaleX(0);
		  opacity: 0;
		  transition: transform 1s, opacity 1s;
		}
		.list-complete-leave-to {
			transform: scaleX(0);
		  opacity: 0;
		  width: 0px;
		  transition: transform 1s, opacity 1s;
		}
		#app {
			margin-top: 3em;
		}
		.list-complete-leave, list-complete-enter-to{
			opacity: 1;
		  transition: transform 1s, opacity 1s;
		}
		.filters {
			margin-top: 1em;
			padding-top: 1em;
			border-top: 1px solid #333333;
		}
	</style>

