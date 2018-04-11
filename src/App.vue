<template>
  <div id="app">
	<DropdownButton/> 
    <div class="row songs">
      <div class="col-3">
		  <Song/> 
	  </div>
	  <div class="col-3">
		  <Song/> 
	  </div>
	  <div class="col-3">
		  <Song/> 
	  </div>
	  <div class="col-3">
		  <Song/> 
	  </div>
	  <div class="col-3">
		  <Song/> 
	  </div>
	  <div class="col-3">
		  <Song/> 
	  </div>
	  <div class="col-3">
		  <Song/> 
	  </div>
	  <div class="col-3">
		  <Song/> 
	  </div>
    </div>
  </div>
</template>

<script>
  import Song from './components/Song'
  import DropdownButton from './components/DropdownButton'
  export default {
    name: 'App',
    components: {
      Song,
      DropdownButton
    }
}
</script>
