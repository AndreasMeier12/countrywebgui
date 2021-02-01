<template>
    <div id="data-table">
        <table class="my-table">
            <tr class="interactive-row" id="data-pop" v-on:click="selectPop()">
                <th class="my-table" id="data-pop-left">Population</th>
                <th class="my-table" id="data-pop-right">{{country['population']}}</th>
                <th class="my-table"><button class="small-button">+</button></th>
            </tr>

            <tr class="my-table" id="data-continent">
                <th class="my-table" id="data-continent-left">Region</th>
                <th class="my-table" id="data-continent-right">{{country['region']}}</th>
                <th></th>
            </tr>

            <tr class="interactive-row" v-on:click="selectArea()" id="data-area" >
                <th class="my-table" id="data-area-left">Area</th>
                <th class="my-table" id="data-area-right">{{country['area']}}</th>
                <th class="my-table"><button class="small-button">+</button></th>

            </tr>


        </table>

    </div>
</template>

<script>
    var country;
    export default {

        name: "data-table",
        props: {
            country
        },
        methods: {
            selectPop() {
                    this.$emit('table:pop');
            },
            selectArea() {
                    this.$emit('table:area');
                },

        },
    }
</script>

<style scoped>
    @import "../assets/styles/shared.css";

</style>