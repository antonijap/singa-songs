<template>
<div class="dropdown-button">
    <label class="language-name" ><input type="checkbox" @click="setValue()" v-model="data.active"/> {{ data.name }}</label>
</div>
</template>

<script>
export default {
  name: 'FilterCheckbox',
  props: {
    data: {
      type: Object,
      required: true
    }
  },
  methods: {
    setValue (){
      this.$root.$emit("setLanguage", {
        key: this.data.code,
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
    .language-name {
      color: black;
      display: inline;
    }
    .dropdown-button{
      padding: 15px;
      display: inline; 
    }
</style>