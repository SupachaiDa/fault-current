<template>
<h1>Fault Current</h1>
<ImgTools/>
<!-- CSS only -->
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.2.0/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-gH2yIJqKdNHPEq0n4Mqa/HGKIhSkIHeL5AyhkYV8i59U5AR6csBvApHHNl/vI1Bx" crossorigin="anonymous">
</template>

<script>
import ImgTools from './components/imgTools.vue'

export default {
  name: 'App',
  components: {
    ImgTools
  }
}
</script>

<style>
  img {
    width: 100px;
  }
</style>
