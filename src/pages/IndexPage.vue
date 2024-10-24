<template>
  <q-page>
    <q-card class="my-card" v-for="(code, index) in codes" :key="index">
      <img :src="tempsImage" height="150" style="width:150px"> 

      <q-card-section>
        <div class="text-h6">LE TEMPS D'AUJOURD'HUI :</div>
        <div class="text-subtitle2">{{temps}}</div>
      </q-card-section>

      <q-card-section class="q-pt-none">
        {{ lorem }}
      </q-card-section>
    </q-card>
  </q-page>
</template>

<script setup>

import axios from 'axios'
import wmoCodes from 'src/data/wmo-codes-fr.json'
import { ref, onMounted } from 'vue'

defineOptions({
  name: 'IndexPage'
})

const temps = ref('')
const tempsImage =ref('')
const dailycodes =ref([])
const codesReference= (wmoCodes)

onMounted(async () => {
  const meteo = await axios.get(`https://api.open-meteo.com/v1/forecast?latitude=48.866667&longitude=2.333333&current=temperature_2m,weather_code&daily=weather_code,temperature_2m_max,temperature_2m_min`)
  const code = meteo.data.current.weather_code
  temps.value = wmoCodes[code].day.description
  tempsImage.value = wmoCodes[code].day.image
  dailycodes.value = config.data.current.currents_units.daily.temperature_2m_max.temperature_2m_min.time.weather_code
  console.log(meteo)
})

</script>
