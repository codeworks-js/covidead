<template>
  <div class="stats">
    <h2><time :datetime="`${date.toISOString().slice(0,10)}`">{{date.toLocaleDateString()}}</time>'s stats</h2>
    <Filter/>
    <transition-group name="countries" tag="ol">
      <li v-for="country in countries" :key="country.Country">
        <CovidBar :country="country"/>
      </li>
    </transition-group>
  </div>
</template>

<script>
import {computed} from 'vue'
import CovidBar from '@/components/CovidBar'
import Filter from '@/components/Filter'

import {useActiveFilter} from '@/state/filter'
import {useCountries} from '@/state/countries'
import {useDate} from '@/state/date'

import {fetchData} from '@/init'

export default {
  name: "CovidStats",
  components: {
    CovidBar,
    Filter,
  },
  setup() {
    const countries = useCountries()
    const date = useDate()
    const filter = useActiveFilter()

    fetchData()

    const orderedCountries = computed(
      () => countries.value.sort(
        (c1, c2) => c2[filter.value.name] - c1[filter.value.name]
      ).filter((country, index) => index < 20)
    )

    return {
      countries: orderedCountries,
      date,
    }
  }
}
</script>

<style scoped>
.stats {
  width: 75%;
  background-color: rgb(240, 240, 240);
  padding: 20px;
  border-radius: 20px;
}

.countries-move {
  transition: transform 0.8s ease;
}

li {
  list-style: none;
}
ol {
  padding-inline-start: unset;
}
</style>
