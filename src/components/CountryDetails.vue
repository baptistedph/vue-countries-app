<template>
  <div class="country-details">
    <img :src="country.flag" />
    <div class="country-info">
      <h3>{{ country.name }}</h3>
      <div>
        <ul>
          <li><span>Native Name: </span>{{ country.nativeName }}</li>
          <li><span>Population: </span>{{ country.population }}</li>
          <li><span>Region: </span>{{ country.region }}</li>
          <li><span>Sub Region: </span>{{ country.subregion }}</li>
          <li><span>Capital: </span>{{ country.capital }}</li>
        </ul>
        <ul>
          <li>
            <span>Top Level Domain: </span
            ><span v-for="tld in country.topLevelDomain" :key="tld">{{
              tld
            }}</span>
          </li>
          <li>
            <span>Currencies: </span
            ><span v-for="currency in country.currencies" :key="currency">{{
              currency.name
            }}</span>
          </li>
          <li>
            <span>Languages: </span
            ><span v-for="language in country.languages" :key="language"
              >{{ language.name }}
            </span>
          </li>
        </ul>
      </div>
      <div class="border-countries">
        <span>Border Countries:</span>
        <div>
          <Button
            v-for="country in country.borders"
            :key="country"
            @click="handleBorderCountryClick(country)"
          >
            {{ country }}
          </Button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Button from '../components/Button.vue'
import { useRoute, useRouter } from 'vue-router'

export default {
  props: ['country', 'getCountry'],
  components: {
    Button,
  },
  setup(props) {
    const router = useRouter()
    const route = useRoute()
    const handleBorderCountryClick = async country => {
      const res = await fetch(
        `https://restcountries.eu/rest/v2/alpha/${country}`,
      )
      const countryWithName = await res.json()
      router.push({
        name: 'Country',
        params: { countryName: countryWithName.name },
      })
    }

    return {
      handleBorderCountryClick,
    }
  },
}
</script>

<style></style>
