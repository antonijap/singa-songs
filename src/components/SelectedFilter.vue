<template>
<div class="selectedFilter">
    <i>{{ dataObj.name }} <i @click="setValue()" class="far fa-times-circle"></i></i>
</div>
</template>

<script>
export default {
  name: 'SelectedFilter',
  props: {
    dataObj: {
      type: Object,
      required: true
    },
    dataType: {
      type: String,
      required: true
    },
  },
   methods: {
    setValue (){
      this.$root.$emit("setFilter", {
        type: this.dataType,
        key: this.dataObj.id,
        active: false
      })

    }
  }
}
</script>

<style lang="scss" scoped>
    .selectedFilter {
        color: white;
        display: inline-block;
        i {
            color: white;
            font-style: normal;
        }
        .fa-times-circle {
            color: white;
        }
        &:not(:last-child) {
          margin-right: 16px;
        }
    }
</style>