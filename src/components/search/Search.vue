<template>
  <div class="search">
    <SearchInput @inputChange="value => handleInputChange(value)" />
    <SearchFilter @selectChange="value => handleSelectChange(value)" />
  </div>
</template>

<script>
import SearchFilter from './SearchFilter.vue'
import SearchInput from './SearchInput.vue'

export default {
  components: {
    SearchFilter,
    SearchInput,
  },
  setup(props, context) {
    const handleInputChange = value => {
      context.emit('inputChange', value)
    }

    const handleSelectChange = value => {
      context.emit('selectChange', value)
    }

    return {
      handleInputChange,
      handleSelectChange,
    }
  },
}
</script>

<style>
@import url('../../assets/css/search.css');
</style>
