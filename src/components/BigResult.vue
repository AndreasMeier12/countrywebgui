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

    </div>
</template>

<script>
    import DataTable from "./DataTable";
    import Plots from "./PopulationPlot";

    var country;
    var allCountries;
    export default {
        props: {
            country,
            allCountries
        },
        components: {
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
                if (this.plot==='population'){
                    this.plot = '';
                } else{
                    this.plot = "population";
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