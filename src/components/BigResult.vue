<template>
    <div id="big-result">

        <div id="big-result-box">
            <div id="big-result-left">
        <h1>{{country['name']}}</h1>
            <img id="big-result-img" :src="country['flag']" :alt="'Flag of' + country['name']">
            </div>
            <div id="big-result-right">
                <data-table v-bind:country="country"/>

            </div>

        </div>
        <plots v-bind:country="country" v-bind:all-countries="allCountries"/>

    </div>
</template>

<script>
    import DataTable from "./DataTable";
    import Plots from "./Plots";

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
            getPopulationPlotData(){
                var pops = this.allCountries.map(x => x['population']).sort();
                return pops;


            }

        }
    }

</script>

<style scoped>
    @import "../assets/styles/shared.css";

</style>