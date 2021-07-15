<template>
  <div class="country-card">
    <router-link
      :to="{
        name: 'Country',
        params: {
          countryName: name,
        },
      }"
    >
      <img class="image" :src="flag" :alt="name" />
      <div class="info">
        <h3>{{ name }}</h3>
        <ul>
          <li v-if="pop"><span>Population: </span>{{ pop }}</li>
          <li v-if="region"><span>Region: </span>{{ region }}</li>
          <li v-if="capital"><span>Capital: </span>{{ capital }}</li>
        </ul>
      </div>
    </router-link>
  </div>
</template>

<script>
export default {
  props: ['flag', 'name', 'pop', 'region', 'capital'],
}
</script>

<style></style>
