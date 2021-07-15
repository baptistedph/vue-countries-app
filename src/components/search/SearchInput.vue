<template>
  <div class="search-input" @click="handleInputFocus">
    <img src="/icons/search.svg" alt="search" />
    <input
      v-model="inputValue"
      ref="input"
      type="text"
      placeholder="Search for a country..."
    />
  </div>
</template>

<script>
import { ref } from '@vue/reactivity'
import { watch } from '@vue/runtime-core'
export default {
  setup(props, context) {
    const inputValue = ref('')

    const input = ref(null)

    watch(inputValue, () => {
      context.emit('inputChange', inputValue.value)
    })

    const handleInputFocus = () => {
      input.value.focus()
    }

    return {
      handleInputFocus,
      input,
      inputValue,
    }
  },
}
</script>

<style></style>
