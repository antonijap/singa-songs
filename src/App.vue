<template>
  <div id="app">
		<div class="row controls">
			<div class="col-md-auto">
					<DropdownButton/>
			</div>
			<div class="col-md-auto">
					<DropdownButton/>
			</div>
		</div>
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

<style lang="scss" scoped>
	.controls {
		padding: 24px 0;
	}
</style>