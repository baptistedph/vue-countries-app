<template>
  <div class="button">
    <slot />
  </div>
</template>

<script>
export default {
  props: ['to'],
}
</script>

<style>
@import url('../assets/css/button.css');
</style>
