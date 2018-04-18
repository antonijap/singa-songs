<template>
    <div v-click-outside="setUnactive">
        <label for="sort">Sort by</label>
        <button class="btn"><span>Popularity <i class="fas" :class=" active ? 'fa-chevron-up' : 'fa-chevron-down' "></i></span></button>
    </div>
</template>

<script>

import FilterCheckbox from './FilterCheckbox.vue'

export default {
  name: 'SortButton',
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
  created () {
   this.$root.$on("activeDropDownChanged", (type) => {
    // Emit to other dropdown elements for active emits
      if(type !== this.filterDataType){
        this.active = false
      }
   }) 
  },
  methods :{
    emitActive(){
        // Emit to other dropdown elements that a element has been activated
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
      padding: 8px 16px;
      position: relative;
      span {
        padding-left: 8px;
      }
      i {
        padding: 0 8px;
      }
    }

    label {
        margin-right: 16px;
    }
</style>

