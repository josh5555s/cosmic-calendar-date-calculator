<template>
  <q-page class="flex flex-center">
    <q-card>
      <q-input
        v-model="yearInput"
        label="Years ago"
        autofocus
        filled
      ></q-input>
      <q-select
        v-model="selectedMultiplier"
        :options="multipliers"
        fill-input
        label="Multiplier"
        filled
      >
      </q-select>
      <div style="padding:10px;"> {{ cosmicDate }}</div>
    </q-card>
  </q-page>
</template>

<script>
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'IndexPage',
  data() {
    return {
      yearInput: 1,
      multipliers: [
        {
          label: 'Billion',
          value: 1000000000
        },
        {
          label: 'Million',
          value: 1000000
        },
        {
          label: 'Thousand',
          value: 1000
        },
      ],
      selectedMultiplier:
      {
        label: 'Billion',
        value: 1000000000
      },
    }
  },
  computed: {
    cosmicDate() {
      const ageOfUniverse = 13797000000  // in years
      const daysInYear = 365
      const yearsInCosmicDay = ageOfUniverse / daysInYear
      const yearsAgo = parseFloat(this.yearInput) * this.selectedMultiplier.value
      const cosmicDaysDecimal = yearsAgo / yearsInCosmicDay
      const cosmicHoursDecimal = cosmicDaysDecimal * 24
      const cosmicHours = Math.floor(cosmicHoursDecimal)
      const cosmicHourRemainderDecimal = cosmicHoursDecimal - cosmicHours
      const cosmicMinutesDecimal = cosmicHourRemainderDecimal * 60
      const cosmicMinutes = Math.floor(cosmicMinutesDecimal)
      const cosmicMinuteRemainderDecimal = cosmicMinutesDecimal - cosmicMinutes
      const cosmicSecondsDecimal = cosmicMinuteRemainderDecimal * 60
      const cosmicSeconds = Math.round(cosmicSecondsDecimal)
      const newYearDate = new Date(2022, 0, 1, 0, 0, 0);

      function subtractTime(date) {
        let d = new Date(date);
        d.setHours(d.getHours() - cosmicHours);
        d.setMinutes(d.getMinutes() - cosmicMinutes)
        d.setSeconds(d.getSeconds() - cosmicSeconds)
        return d;
      }

      const cosmicDatetime = subtractTime(newYearDate)

      return cosmicDatetime
    }
  }
})
</script>
