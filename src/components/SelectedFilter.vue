<template>
<div class="selectedFilter">
    <span @click="setValue()"> {{ dataObj.name }} </span>
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
        cursor: pointer;
        span {
          font-style: normal;
          color: white;
          border-radius: 100%;
          position: relative;
          vertical-align: middle;
          font-size: 16px;
          line-height: 23px;
          &:after {
            content: '×';
            position: relative;
            width: 15px;
            height: 15px;
            border-radius: 100%;
            background: #333333;
            color:#BDBDBD;
            display: inline-block;
            vertical-align: middle;
            line-height: 15px;
            text-align: center;
          }
        }
        &:not(:last-child) {
          margin-right: 16px;
        }
    }
</style>