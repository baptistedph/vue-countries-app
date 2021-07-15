<template>
  <div class="search-filter">
    <select v-model="selectValue">
      <option disabled>Filter by Region</option>
      <option selected value="all">All</option>
      <option value="africa">Africa</option>
      <option value="americas">Americas</option>
      <option value="asia">Asia</option>
      <option value="europe">Europe</option>
      <option value="oceania">Oceania</option>
    </select>
  </div>
</template>

<script>
import { ref } from '@vue/reactivity'
import { watch } from '@vue/runtime-core'
export default {
  setup(props, context) {
    const selectValue = ref('all')

    watch(selectValue, () => {
      context.emit('selectChange', selectValue.value)
    })

    return {
      selectValue,
    }
  },
}
</script>

<style></style>
