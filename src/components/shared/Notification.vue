<template lang="pug">
  .container
    .columns
      .column.is-5.is-offset-4
        .notification(:class="{'is-success': isSucceed, 'is-danger': !isSucceed }")
          slot(name="body") mensaje
</template>

<style lang="scss" scoped>
  .notification {
    margin: 10px;
  }
</style>


<script>
  export default {
    props:{
      isSucceed: {
        Type: Boolean,
        
      }
    },
  }
</script>
