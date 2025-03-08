<script lang="ts" setup>
import { computed } from 'vue'

const props = defineProps({
  number: {
    type: String,
  },
  letters: {
    type: String,
    default: '',
  },
  frequencies: {
    type: Array<number>,
    default: () => [],
  },
  gain: {
    type: Number,
    default: 1,
  },
})

const audioContext = new AudioContext()
const gainNode = computed(() => {
  const node = audioContext.createGain()
  node.connect(audioContext.destination)
  node.gain.value = props.gain
  return node
})

let oscs: OscillatorNode[] = []

const onPressed = () => {
  oscs = props.frequencies.map((freq) => {
    const osc = audioContext.createOscillator()
    osc.setPeriodicWave(audioContext.createPeriodicWave([0, 1], [0, 0]))
    osc.frequency.value = freq
    osc.connect(gainNode.value)
    return osc
  })
  oscs.forEach((osc) => {
    osc.start()
  })
}

const onReleased = () => {
  oscs.forEach((osc) => {
    osc.stop()
  })
}
</script>

<template>
  <button
    class="aspect-square rounded-full bg-orange-400 p-2 text-6xl transition-all hover:cursor-pointer hover:brightness-95 active:brightness-90"
    type="button"
    @mousedown="onPressed"
    @mouseup="onReleased"
  >
    <span>{{ props.number }}</span>
  </button>
</template>
