<script lang="ts" setup>
import DialButton from '@/components/DialButton.vue'
import { computed, ref } from 'vue'

const dialFrequencies = ref([
  {
    key: '1',
    frequencies: [697, 1209],
  },
  {
    key: '2',
    frequencies: [697, 1336],
  },
  {
    key: '3',
    frequencies: [697, 1477],
  },
  {
    key: '4',
    frequencies: [770, 1209],
  },
  {
    key: '5',
    frequencies: [770, 1336],
  },
  {
    key: '6',
    frequencies: [770, 1477],
  },
  {
    key: '7',
    frequencies: [852, 1209],
  },
  {
    key: '8',
    frequencies: [852, 1336],
  },
  {
    key: '9',
    frequencies: [852, 1477],
  },
  {
    key: '*',
    frequencies: [941, 1209],
  },
  {
    key: '0',
    frequencies: [941, 1336],
  },
  {
    key: '#',
    frequencies: [941, 1477],
  },
])

const gain = ref(50)

const computedGain = computed(() => gain.value / 100.0)
</script>

<template>
  <main class="mr-auto ml-auto grid w-1/2 grid-cols-3 gap-4 p-4 md:w-1/3">
    <label class="col-start-1 col-end-2 mr-auto ml-auto" for="gain">Gain</label>
    <input
      id="gain"
      v-model="gain"
      class="col-start-2 col-end-4 mb-6 appearance-none rounded-full border border-orange-300"
      max="100"
      min="0"
      type="range"
    />
    <dial-button
      v-for="k in dialFrequencies"
      :key="k.key"
      :frequencies="k.frequencies"
      :gain="computedGain"
      :number="k.key"
    ></dial-button>
    <div class="col-start-1 col-end-4 mt-4 rounded-lg bg-orange-200 p-4">
      For iOS devices, make sure you either use headphones or turn off silent mode.
    </div>
  </main>
</template>
