<template>

<div>
  <div class="dropdown-button">
    <button @click="active = !active" :class=" active ? 'active' : '' " class="btn btn-default" type="submit">{{ title }}
      <!-- you can dynamically bind classes as below, changing the icon depending on active data property -->
      <i class="fas" :class=" active ? 'fa-chevron-up' : 'fa-chevron-down' "></i>
    </button>
  </div>
  <transition name="fadein">
    <div class="container" v-if="active">
      <div class="row dropdown-options">
        <div class="col col-sm-6" v-for="lang in languages">
          <div class="form-group">
            <FilterCheckbox  :data="lang" :key="lang.code"/>
          </div>
        </div>
      </div>
    </div>
  </transition>
  
</div>

</template>

<script>

import FilterCheckbox from './FilterCheckbox.vue'

export default {
  name: 'DropdownButton',
  components: {
    FilterCheckbox
  },
  props: {
    title: {
      type: String,
      required: true
    },
    languages: {
      type: Array,
      required: true
    }
  },
  data () {
    return {
      active: false
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

    .dropdown-options {
		background: white;
		padding: 24px;
		position: absolute;
		width: 400px;
		border-radius: 8px;
		margin-top: 8px;
		z-index: 9999;
    }   

	.fadein-enter-active {
		animation: flip-in .2s;
		z-index: 999;
	}

	.fadein-leave-active {
		animation: flip-in .2s reverse;
		z-index: 999;
	}

	@keyframes flip-in {
		0% {
			opacity: 0%;
			transform: translateY(-10px)
		}
		100% {
			opacity: 100%;
			transform: translateY(0px)
		}
	}

	.active {
		background: #828282;
	}
</style>