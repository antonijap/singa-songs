<template>
<div class="dropdown-button">
    <button class="btn btn-default" type="submit">Button <i class="fas fa-chevron-down"></i></button>
</div>
</template>

<script>
export default {
  name: 'DropdownButton',
  data () {
    return {
      title: 'Cry',
      artist: 'Pink',
      genre: 'pop'
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
        font-size: 16px;
        letter-spacing: -0.2px;
        font-family: "Basier Square";
        font-weight: 500;
    }   
</style>