<template>
    <div id="big-result">

        <div id="big-result-box">
            <div id="big-result-left">
        <h1>{{country['name']}}</h1>
            <img id="big-result-img" :src="country['flag']" :alt="'Flag of' + country['name']">
            </div>
            <div id="big-result-right">
                <data-table v-bind:country="country" @table:area="showAreaPlot" @table:pop="showPopulationPlot" @table:noplot="showNoPlot"/>

            </div>

        </div>
        <plots v-if="this.plot==='population'" v-bind:country="country" v-bind:all-countries="allCountries"/>
        <area-plot v-if="this.plot==='area'" v-bind:country="country" v-bind:all-countries="allCountries"/>

    </div>
</template>

<script>
    import DataTable from "./DataTable";
    import Plots from "./PopulationPlot";
    import AreaPlot from "./AreaPlot";

    var country;
    var allCountries;
    export default {
        props: {
            country,
            allCountries
        },
        components: {
            AreaPlot,
            Plots,
            DataTable


        },
        methods: {
            showPopulationPlot(){
                if (this.plot==='population'){
                    this.plot = '';
                } else{
                    this.plot = "population";
                }
            },
            showAreaPlot(){
                if (this.plot==='area'){
                    this.plot = '';
                } else{
                    this.plot = "area";
                }
            },
            showNoPlot(){
                this.plot = "";
            },


        },
        data() {
            return {
                plot: ""
            }
        }
    }

</script>

<style scoped>
    @import "../assets/styles/shared.css";

</style>