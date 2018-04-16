<template>
  <div class="spinner">
    
  </div>

</template>
<script>
  export default {
    name: 'LoadingSpinner'


}
</script>
<style lang="scss">
  .spinner {
     border: 2px solid #f6502b;
     font-size: 40px;
     width: 1em;
     height: 1em;
     border-radius: 0.5em;
     box-sizing: border-box;
     animation: spin 1s linear infinite;
     border-top-color: #ed2525;
     margin: 0 auto;
  }
   @-moz-keyframes spin {
     to {
       transform: rotate(360deg);
       border-left: 0;
    }
  }
   @-webkit-keyframes spin {
     to {
       transform: rotate(360deg);
       border-left: 0;
    }
  }
   @-o-keyframes spin {
     to {
       transform: rotate(360deg);
       border-left: 0;
    }
  }
   @keyframes spin {
     to {
       transform: rotate(360deg);
       border-left: 0;
    }
  }
 
    
</style>