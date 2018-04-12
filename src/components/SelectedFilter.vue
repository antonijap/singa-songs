<template>
<div class="selectedFilter">
    <i>{{ title }} <i class="far fa-times-circle"></i></i>
</div>
</template>

<script>
export default {
  name: 'SelectedFilter',
  props: {
    title: {
      type: String,
      required: true
    }
  }
}
</script>

<style lang="scss" scoped>
    .selectedFilter {
        color: white;
        i {
            color: white;
            font-style: normal;
        }
        .fa-times-circle {
            color: white;
        }
    }
</style>