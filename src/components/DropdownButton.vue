<template>

<div>
  <div class="dropdown-button">
    <button class="btn btn-default" type="submit">{{ title }}
      <i class="fas fa-chevron-down"></i>
    </button>
  </div>
  <div class="container">
    <div class="row dropdown-options">
      <div class="col col-sm-6">
        <div class="form-group">
          <input type="checkbox" class="form-check-input">
          <label>Finnish</label>
        </div>
      </div>
      <div class="col col-sm-6">
        <div class="form-group">
          <input type="checkbox" class="form-check-input">
          <label>Swedish</label>
        </div>
      </div>
      <div class="col col-sm-6">
        <div class="form-group">
          <input type="checkbox" class="form-check-input">
          <label>German</label>
        </div>
      </div>
      <div class="col col-sm-6">
        <div class="form-group">
          <input type="checkbox" class="form-check-input">
          <label>Spanish</label>
        </div>
      </div>
    </div>
  </div>
</div>

</template>

<script>
export default {
  name: 'DropdownButton',
  props: {
    title: {
      type: String,
      required: true
    }
  }
}
</script>

<style lang="scss" scoped>
    .btn {
        border-radius: 100px;
        background: #333333;
        color: white;
        border: none;
        padding: 8px 24px;
        position: relative;
    }
	.form-group {
		label {
			margin-bottom: 0;
		}
	}
    .dropdown-options {
      background: white;
      padding: 24px;
	  position: fixed;
      border-radius: 8px;
      margin-top: 8px;
      z-index: 9999;
    }   
</style>