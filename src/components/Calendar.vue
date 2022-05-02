<template>
    <div class="container">
        <div>Mes: {{months[month]}} de {{year}} - {{month}}</div>
        <div class="columns-7">
            <div v-for="d in days" :key="d"
            class="p-2 text-center">
                {{d}}</div>
        </div>
        <div class="columns-7"
            v-for="row in nroRows" :key="row">
            <div v-for="col in 7" :key="col"
                class="columns-7 py-1 bg-teal-50">
                    <button
                        class="border w-full"
                        @click="setDay(row,col)"
                        v-if="getDay(row,col) > 0 && getDay(row,col) <= endOf"
                    >{{getDay(row,col)}}</button>
                    <span v-else>-</span>
            </div>
        </div>
    </div>
</template>
<script>
import moment from 'moment'

export default {
    props: ['refDate','dropOff','pickUp'],
    data: ()=>({
        days: ['L','M','M','J','V','S','D'],
        months: ['Enero','Febrero','Marzo','Abril','Mayo','Junio','Julio',
                 'Agosto','Septiembre','Octubre','Noviembre','Diciembre'],
    }),
    created() {
        //this.refDate = today
    },

    computed: {
        month() {
            return moment(this.refDate).format('M') - 1;//this.refDate.getMonth()
        },
        year() {
            return moment(this.refDate).format('YYYY');//this.refDate.getMonth()
        },
        startOf() {
            const day = moment(this.refDate).startOf('month')
            return parseInt(moment(day).day());
        },
        endOf() {
            const day = moment(this.refDate).endOf('month')
            return parseInt(moment(day).format("D"));
        },
        nroRows() {
            const tot = this.endOf + this.startOf - 1
            const mod = tot % 7
            const div = (tot - mod) / 7
            return mod > 0 ? div + 1 : div
        },
        
    },

    methods: {
        getDay(row,col) {
            return (((row - 1) * 7) + col) - (this.startOf - 1)
        },
        setDay(row,col) {
            const getDay = this.getDay(row,col);
            const day = getDay < 10 ? '0' + getDay : getDay
            const months = ['01','02','03','04','05','06','07','08','09','10','11','12',]
            this.$emit('setDay',`${this.year}-${months[this.month]}-${day}`)
            console.log(`${this.year}-${months[this.month]}-${day}`)
            //this.$emit('setDay', day)
            // if (this.start && this.end) {
            //     //si ambos
            //     this.start = day
            //     this.end = null
            // } else
            //     this.start
            //         ? day < this.start ? this.start = day : this.end = day
            //         : this.start = day
        },
    }

}
</script>