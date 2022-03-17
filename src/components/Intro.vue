<template>
  <div id="intro">
    <h2>{{ header }}</h2>
    <p v-html="body">
    </p>
  </div>
</template>

<script>
export default {
  props: ['header', 'body']
}
</script>

<style lang="scss">
@import url('../styles/intro.scss');
</style>