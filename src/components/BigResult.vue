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
    </div>
</template>

<script>
    import DataTable from "./DataTable";
    var country;
    export default {
        props: {
            country
        },
        components: {
            DataTable


        }
    }

</script>

<style scoped>
    @import "../assets/styles/shared.css";

</style>