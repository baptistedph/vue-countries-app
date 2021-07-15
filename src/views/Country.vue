<template>
  <div class="country">
    <Button @click="handleGoBack">
      <img class="icon" src="/icons/back.svg" />
      Back
    </Button>
    <CountryDetails
      v-if="country"
      :getCountry="getCountry"
      :country="country[0]"
    />
    <div class="loading" v-else>Loading...</div>
  </div>
</template>

<script>
import { ref } from '@vue/reactivity'
import Button from '../components/Button.vue'
import CountryDetails from '../components/CountryDetails.vue'
import { useRoute, useRouter } from 'vue-router'
import { watchEffect } from '@vue/runtime-core'

export default {
  props: ['countryName'],
  components: {
    Button,
    CountryDetails,
  },
  setup(props) {
    const country = ref(null)

    const route = useRoute()
    const router = useRouter()

    const getCountry = async () => {
      const res = await fetch(
        'https://restcountries.eu/rest/v2/name/' + props.countryName,
      )
      country.value = await res.json()
    }

    const handleGoBack = () => {
      router.go(-1)
    }

    watchEffect(getCountry, route)

    return { country, getCountry, handleGoBack }
  },
}
</script>

<style>
@import url('../assets/css/country.css');

.loading {
  position: absolute;
  z-index: 99;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
}
</style>
