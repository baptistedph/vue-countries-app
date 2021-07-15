<template>
  <div class="country-cards">
    <CountryCard
      v-for="country in filteredCountries"
      :key="country.name"
      :flag="country.flag"
      :name="country.name"
      :pop="country.population"
      :region="country.region"
      :capital="country.capital"
    />
  </div>
</template>

<script>
import { ref } from '@vue/reactivity'
import CountryCard from './CountryCard.vue'
import { watchEffect } from '@vue/runtime-core'

export default {
  components: {
    CountryCard,
  },
  props: ['options'],
  setup(props) {
    const countries = ref([])

    const filteredCountries = ref([])

    watchEffect(() => {
      if (props.options.name) {
        if (props.options.region && props.options.region !== 'all') {
          filteredCountries.value = countries.value.filter(
            country =>
              country.name
                .toLowerCase()
                .includes(props.options.name.toLowerCase()) &&
              country.region.toLowerCase() ===
                props.options.region.toLowerCase(),
          )
        } else {
          filteredCountries.value = countries.value.filter(country =>
            country.name
              .toLowerCase()
              .includes(props.options.name.toLowerCase()),
          )
        }
      } else if (props.options.region && props.options.region !== 'all') {
        filteredCountries.value = countries.value.filter(
          country =>
            country.region.toLowerCase() === props.options.region.toLowerCase(),
        )
      } else {
        filteredCountries.value = countries.value
      }
    }, props.options)

    const getCountries = async () => {
      const res = await fetch('https://restcountries.eu/rest/v2/all')
      countries.value = await res.json()
    }

    getCountries()

    return { countries, filteredCountries }
  },
}
</script>

<style>
@import url('../../assets/css/country-cards.css');
</style>
