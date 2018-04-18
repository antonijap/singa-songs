<template>
<div class="dropdown-button">
    <input type="checkbox" v-model="data.active"/>
    <label class="language-name" v-bind:class="{ active: data.active }" @click="setValue()"> {{ data.name }}</label>
</div>
</template>

<script>
export default {
  name: 'FilterCheckbox',
  props: {
    data: {
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
        key: this.data.id,
        active: !this.data.active
      })
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
        display: inline;
    }   
    .dropdown-button {
      display: inline-block;
      width: 100%;
      .active {
        font-weight: 500;
      }
      .language-name {
        color: black;
        position: relative;
        margin-bottom: 0;
        font-size: 16px;
        line-height: 16px;
        padding: 8px 0 8px 28px;
        cursor: pointer;
        &:before {
          content: '';
          width: 14px;
          height: 14px;
          border: 1px solid #BDBDBD;
          position: absolute;
          left: 0;
          border-radius: 2px;
        }
      }
      input {
        display: none;
      }
      input:checked + .language-name:before {
        background: url('../assets/check.svg') no-repeat center center;
        border-color: transparent;
      }
    } 
</style>