<template>
  <li>
    <h2><a :href="artist.url" target="_blank">{{artist.name}}</a></h2>
    <img :src="artist.image[2]['#text']" alt="">
  </li>
</template>

<script>
export default {
  name: 'Artist',
  props: [ 'artist' ]
}
</script>

<style lang="scss">
  li { display: block; margin: 10px 0;}
</style>
