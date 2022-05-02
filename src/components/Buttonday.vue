<template>
    <button
        v-if="visible"
        @click="setDay"
        :disabled="disabled"
        class="btn btn-success">
        {{day}}</button>
</template>
<script>
import moment from 'moment'
export default {
    props: ['row','col','startOf','endOf','month', 'year'],
    computed: {
        visible() {
            return this.day > 0 && this.day <= this.endOf
        },
        day() {
            return (((this.row - 1) * 7) + this.col) - (this.startOf - 1)
        },
        disabled() {
            return this.month == moment().format('M')
                ? this.day < moment().format('D')
                : false
        },
    },
    methods: {
        setDay() {
            const months = ['01','02','03','04','05','06','07','08','09','10','11','12',]
            const day = this.day < 10 ? '0' + this.day : this.day
            this.$emit('setDay',`${this.year}-${months[this.month]}-${day}`)
        }
    }
}
</script>