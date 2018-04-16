<template>

<div v-click-outside="setUnactive">
  <div class="dropdown-button">
    <button @click="active = !active; emitActive()"  class="btn btn-default" type="submit" v-bind:class="{ active: active }">
	{{ title }} <i class="fas" :class=" active ? 'fa-chevron-up' : 'fa-chevron-down' "></i>
      <!-- you can dynamically bind classes as below, changing the icon depending on active data property -->
    </button>
  </div>
  <transition name="fadein">
    <div class="container" v-if="active">
      <div class="row dropdown-options">
        <div class="col col-sm-6" v-for="item in filterData">
          <div class="form-group">
            <FilterCheckbox  :data="item" :key="item.id" :dataType="filterDataType"/>
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
    filterData: {
      type: Object,
      required: true
    },
    filterDataType: {
      type: String,
      required: true
    }
  },
  data () {
    return {
      active: false
    }
  },
  // computed : {
  //   dataType () {
  //     console.log(this.languages , this.genres )
  //     return this.languages | this.genres 
  //   }
  // },
  created () {
   this.$root.$on("activeDropDownChanged", (type) => {
    //emit to other dropdown elements for active emits
      if(type !== this.filterDataType){
        this.active = false
      }
   }) 
  },
  methods :{
    emitActive(){
        //emit to other dropdown elements that a element has been activated
       this.$root.$emit("activeDropDownChanged", this.filterDataType)
    },
    setUnactive() {
      this.active = false
    }
  },
  directives: {
      
      'click-outside': {

        bind: function (el, binding, vnode) {
          el.event = function (event) {
            if (!(el == event.target || el.contains(event.target))) {
              vnode.context[binding.expression](event);
            }
          };
          document.body.addEventListener('click', el.event)
        },
        unbind: function (el) {
          document.body.removeEventListener('click', el.event)
        }
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
			opacity: 0;
			transform: translateY(-10px)
		}
		100% {
			opacity: 1;
			transform: translateY(0px)
		}
	}

	.active {
		background: #828282;
	}
</style>

