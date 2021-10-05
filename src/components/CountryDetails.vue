<template>
  <div class="country-details">
    <img :src="country.flags.svg" />
    <div class="country-info">
      <h3>{{ country.name.common }}</h3>
      <div>
        <ul>
          <li>
            <span>Native Name: </span
            >{{ Object.values(country.name.nativeName)[0].common }}
          </li>
          <li><span>Population: </span>{{ country.population }}</li>
          <li><span>Region: </span>{{ country.region }}</li>
          <li><span>Sub Region: </span>{{ country.subregion }}</li>
          <li><span>Capital: </span>{{ country.capital[0] }}</li>
        </ul>
        <ul>
          <li>
            <span>Top Level Domain: </span
            ><span v-for="tld in country.tld" :key="tld">{{ tld }}</span>
          </li>
          <li>
            <span>Currencies: </span
            ><span v-for="currency in country.currencies" :key="currency">{{
              currency.name
            }}</span>
          </li>
          <li>
            <span>Languages: </span
            ><span v-for="language of country.languages" :key="language"
              >{{ language }}
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
import { useRouter } from 'vue-router'

export default {
  props: ['country', 'getCountry'],
  components: {
    Button,
  },
  setup(props) {
    const router = useRouter()

    const handleBorderCountryClick = async country => {
      const res = await fetch(`https://restcountries.com/v3.1/alpha/${country}`)
      const countryWithName = await res.json()
      router.push({
        name: 'Country',
        params: { countryName: countryWithName[0].name.common },
      })
    }

    return {
      handleBorderCountryClick,
    }
  },
}
</script>

<style></style>
