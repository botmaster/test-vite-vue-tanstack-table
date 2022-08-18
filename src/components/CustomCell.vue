<template>
  <div><p>Ma super custom cell !!!
    <br>super value: {{value}}</p></div>
</template>

<script>
export default {
  name: "CustomCell",
  props: {
    value: {
      type: String,
      default: 'na'
    },
  },
}
</script>

<style scoped>
  p {
    font-size: 10px;
    color: red;
    margin-top: 0;
    margin-bottom: 0;
  }

  p + p {
    margin-top: 10px
  }
</style>