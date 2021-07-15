<template>
  <Search
    @inputChange="value => handleInputChange(value)"
    @selectChange="value => handleSelectChange(value)"
  />
  <CountryCards :options="{ name, region }" />
</template>

<script>
import Search from '../components/search/Search.vue'
import CountryCards from '../components/country-cards/CountryCards.vue'
import { ref } from '@vue/reactivity'

export default {
  components: {
    Search,
    CountryCards,
  },
  setup() {
    const name = ref('')
    const region = ref('')

    const handleInputChange = value => {
      name.value = value
    }

    const handleSelectChange = value => {
      region.value = value
    }

    return {
      handleInputChange,
      handleSelectChange,
      name,
      region,
    }
  },
}
</script>
