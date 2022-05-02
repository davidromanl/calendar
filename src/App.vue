<template>
  <div class="container">
    <div class="columns-2">
      <div>pickUp: {{pickUp}}</div>
      <div>dropOff: {{dropOff}}</div>
    </div>
    <hr>
    <div class="container">
      <div class="columns-3">
          <div class="items-center">
            <button
              class="rounded bg-stone-400 border px-2"
              :disabled="month==0"
              @click="changeMonth(-1)">Prev</button>
          </div>
          <div class="text-center">
            <strong>Mes: {{month}}</strong>
          </div>
          <div class="items-center">
            <button
              class="rounded bg-stone-400 border px-2"
              :disabled="month==30"
              @click="changeMonth(1)">Next</button>
          </div>
      </div>
      <div class="columns-2">
          <div class="col">
            <Calendar
              @setDay="setDay"
              :dropOff="dropOff"
              :pickUp="pickUp"
              :refDate="refDate(month)"/>
          </div>
          <div class="col">
            <Calendar
              @setDay="setDay"
              :dropOff="dropOff"
              :pickUp="pickUp"
              :refDate="refDate(month + 1)"/>
          </div>
      </div>
    </div>
  </div>
</template>

<script>
import moment from 'moment'
import Calendar from "./components/Calendar.vue"
const today = moment().format()
export default {
  name: 'App',
  data: () => ({
    month: 0,
    pickUp: null,
    dropOff: null
  }),
  components: {
    Calendar
  },
  methods: {
    refDate(month) {
      const day = moment(today).add(month, 'M')
      return moment(day).format('YYYY-MM-DD')
    },
    changeMonth(i) {
      this.month = this.month + i
    },
    setDay(day) {
      this.pickUp = day
      console.log(day)
    }
  }
}
</script>

<style>

</style>
