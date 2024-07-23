<script setup>
import CountdownHeader from '@/projects/newYearsCountdown/components/CountdownHeader.vue'
import CountdownSegment from '@/projects/newYearsCountdown/components/CountdownSegment.vue'
import { onMounted, onUnmounted, reactive, watch } from 'vue'

const timeRemaining = reactive({
  days: 0,
  hours: 0,
  minutes: 0,
  seconds: 0
})

const calculateTimeRemaining = () => {
  const now = new Date()
  const nextYear = new Date(now.getFullYear() + 1, 0, 1)
  const diff = nextYear - now

  const days = Math.floor(diff / (1000 * 60 * 60 * 24))
  const hours = Math.floor((diff % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60))
  const minutes = Math.floor((diff % (1000 * 60 * 60)) / (1000 * 60))
  const seconds = Math.floor((diff % (1000 * 60)) / 1000)

  timeRemaining.days = days
  timeRemaining.hours = hours
  timeRemaining.minutes = minutes
  timeRemaining.seconds = seconds
}

watch(
  [
    () => timeRemaining.days,
    () => timeRemaining.hours,
    () => timeRemaining.minutes,
    () => timeRemaining.seconds
  ],
  ([newDays, newHours, newMinutes, newSeconds], [oldDays, oldHours, oldMinutes, oldSeconds]) => {}
)

let intervalId

onMounted(() => {
  calculateTimeRemaining()
  intervalId = setInterval(calculateTimeRemaining, 1000)
})

onUnmounted(() => {
  clearInterval(intervalId)
})
</script>
<template>
  <div class="app-wrapper">
    <div class="countdown-box">
      <CountdownHeader />
      <main class="flex justify-center">
        <CountdownSegment data-test="days" label="days" :number="timeRemaining.days" />
        <CountdownSegment data-test="hours" label="hours" :number="timeRemaining.hours" />
        <CountdownSegment data-test="minutes" label="minutes" :number="timeRemaining.minutes" />
        <CountdownSegment data-test="seconds" label="seconds" :number="timeRemaining.seconds" />
      </main>
    </div>
  </div>
</template>

<style scoped>
.app-wrapper {
  @apply flex items-center justify-center w-full h-full p-10;
}
.countdown-box {
  @apply shadow-md relative bg-white p-5 rounded-lg border-gray-100 border-[1px];
}
body {
  @apply bg-gray-100;
}
</style>
